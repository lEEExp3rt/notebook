# C in Linux

---
## GCC
### GCC支持编译的后缀名
|后缀名|对应文件类型|
| :---: | :---: |
|.c|C原始程序|
|.C<br>.cc<br>.cxx|C++原始程序|
|.m|Objective-C原始程序|
|.s<br>.S|汇编语言原始程序|
|.i|已经过预处理的C原始程序|
|.ii|已经过预处理的C++原始程序|
|.h|预处理文件（头文件）|
|.o|目标文件|
|.a<br>.so|编译后的库文件|
### 编译过程
编译过程分为预处理、编译、汇编、链接
以下代码介绍从`main.c`开始

1. 预处理：宏替换、头文件展开、预编译指令处理、删除注释等
```bash
gcc -E main.c #仅进行预处理，无生成目标文件
gcc -E main.c -o main.i #生成预处理文件main.i
gcc main.c -o main.i -E #同上
```

2. 编译：检查语法、代码优化、汇总符号、生成汇编代码等
```bash
gcc -S main.i
gcc -S main.i -o main.s
gcc main.i -o main.s -S
```

3. 汇编：合并各section、生成.o文件等
```bash
gcc -c main.s
gcc -c main.s -o main.o
gcc main.s -o main.o -c
```

4. 链接：合并各obj文件的section，合并符号表，符号地址重定位，生成可执行文件
```bash
gcc main.o -o main.out
```
其中，在预处理阶段进行了头文件包含的操作，在链接阶段gcc会在没有参数指定时到Linux系统默认路径`/usr/lib`下查找**库文件**，将函数链接到*libc.so.6*库函数中去
gcc在编译时默认使用动态链接库，编译链接时不把库文件代码加入可执行文件中，而是在程序执行的时候动态加载链接库，以节省系统开销
### 参数使用
#### 总体参数
* `-E`：只进行预处理
* `-S`：只编译不会变，生成汇编代码
* `-c`：只编译不链接，生成目标文件
* `-o file`：将文件输出到目标文件*file*中
* `-g`：在可执行程序中包含调试信息
* `-v`：显示gcc版本信息
* `-I dir`：在**头文件**的搜索路径中添加*dir*目录
* `-L dir`：在**库文件**的搜索路径列表中添加*dir*目录
* `-static`：链接静态库
* `-llibrary`：链接名为*library*的库文件
说明：
1. 当头文件与gcc不在同一目录下时要用`-I dir`参数，它指头文件所在的目录
2. 添加库文件时用`-L dir`参数，它指定库文件所在的目录
3. 头文件包含语句`include<file>`，`<headerfile>`表示在默认路径`/usr/include`中寻找头文件，`"headerfile"`表示在指定的目录中寻找。如果`"headerfile"`在当前目录下，则可以省略`-I dir`参数
4. 参数`-L dir`指定的是路径而不是文件，所以需要指定文件就需要`-llibrary`参数。Linux系统下库文件的命名规定必须以*lib*开头，因此在使用`-l`指定链接库文件时可以省去*lib*三个字母，如`-llibsunq`可以省略为`-lsunq`
5. 使用`cpp -v`命令查看标准系统头文件的路径
基本上默认路径为：
```bash{.line-numbers}
usr/include
usr/lib/include
usr/local/include
```

#### 报警参数
* `-ansi`：支持符合ANSI的C程序
* `-pedantic`：允许发出ANSI C标准所列的全部告警信息
* `-pedantic-error`：允许发出ANSI C标准所列的全部报错信息
* `-w`：关闭所有告警
* `-Wall`：允许发出gcc提供的所有有用的告警信息
* `-werror`：把所有告警信息转化为错误信息，并在告警发生时终止编译

#### 优化参数
代码优化是指编译器通过分析源代码找出未达到最优的部分对其重新组合以改善程序的执行性能
编译参数：`-On`，其中n取值及优化效果在不同版本的gcc是不完全相同的，典型的取值是0（不优化），1，2，3，s
在Linux系统下使用`time`命令来大致统计程序运行所需时间

---
## 函数库
### 存放路径
标准系统库文件通常存放在`/lib`和`/usr/lib`下
### 命名规范
库文件总是以*lib*开头，随后部分指明是什么库（c代表C语言库，m代表数学库），文件名最后部分以.开始，然后给出库文件类型（.a代表静态函数库，.so代表共享函数库）
> 例：libm.a代表静态数学函数库

可以通过给出完整路径名或`-l`指示编译器要搜索的库文件
```bash{.line-numbers}
gcc -o hello hello.c /usr/lib/libm.a
#等价于
gcc -o hello hello.c -lm #这里-lm是简写，代表/usr/lib中libm.a

#也可通过-L参数为编译器增加库的搜索路径
gcc -o x11pro1 x11hello.c -L/usr/openwin/lib -lX11 #调用libX11库
```
`-l`的另一个好处在如果有共享库，编译器会自动选择共享库
### 静态库
创建和维护静态库很容易，只要使用`ar`（代表archive，建立归档文件）程序和`gcc -c`命令对函数分别进行编译即可
应该尽可能把函数分别保存知道不同的源文件中，除非函数需要访问公共数据，此时放在同一个源文件中并使用在该文件中声明的静态变量
##### 创建静态库
1. 创建函数源文件
2. 使用`gcc-c`生成`.o`文件
3. 创建头文件`.h`，包含函数的声明
4. 使用`ar`程序创建一个归档文件并添加目标文件<br>`-c`:Create the archive 创建归档文件<br>`-r`：Insert the files member... into archive (with replacement) 添加目标文件<br>`-v`：显示操作信息如添加的文件和每个文件的详细信息
5. 调用函数库，使用`gcc`编译并用`-L`和`-l`参数

```bash{.line-numbers}
#例
root@localhost ~> cat pro1.c
#include<stdio.h>
int pro1(int argv)
{
    printf("hello,%d\n",argv);
    return 0;
}

root@localhost ~> cat pro2.c
#include<stdio.h>
int pro2(char *argv)
{
    printf("Hello, %s\n",argv);
    return 0;
}

root@localhost ~> gcc -c pro1.c pro2.c

root@localhost ~> ls *.o
pro1.o  pro2.o

root@localhost ~> cat lib.h
int pro1(int);
int pro2(char *);

root@localhost ~> ar crv libfoo.a pro1.o pro2.o
a - pro1.o
a - pro2.o

root@localhost ~> cat hello.c
#include "lib.h"
int main()
{
    pro2("Linux world");
    exit(0);
}

root@localhost ~> gcc -o hello hello.c -L. -lfoo -w

root@localhost ~> ./hello
Hello, Linux world
``` 

### 共享库
静态库有一个缺点，即同时运行的多个程序都使用来自同一个库的函数时会出现同一函数的多份拷贝，这会导致占用大量内存和存储
共享库可以用来实现函数的动态链接，以克服这种不足
```bash{.line-numbers}
root@localhost ~> cat hello.c
#include<stdio.h>
#include<math.h>
int main()
{
    double a,b;
    a=3.14;
    b=sin(a);
    printf("%lf %lf",a,b);
    return 0;
}

root@localhost ~> gcc hello.c -o hello
/usr/bin/ld: /tmp/cc8o3n0H.o: in function `main':
hello.c:(.text+0x23): undefined reference to `sin'
collect2: error: ld returned 1 exit status
```
这里直接编译出现了错误，因为虽然包含了数学函数库，但没有指定函数的具体路径
可以使用`nm`命令进行查找
Linux系统下的`nm`命令主要用于列出目标文件中的符号引证解释，可以用来查看目标文件中的各个符号的详细信息
```bash
root@localhost ~> nm -o /lib/*.so|grep sin
/lib/libm-2.3.2.so:00008610 W sin
/lib/libm-2.3.2.so:00008610 t _sin

root@localhost ~> gcc hello.c -o hello -lm

root@localhost ~> ./hello
3.140000 0.001593
```
注意在不同系统中，*lib*存放位置可能不同
在Windows系统下，.so库对应.DLL文件，而.a库类似于.LIB文件，包含在可执行程序中

---
## Make
### Make参数
基本格式：
```bash
make [options] [filename]
```
参数选项：
* `-d`：显示调试信息
* `-f file`：指定*file*作为依赖关系文件而不是默认的*makefile*或*Makefile*，如果指定文件名为“-”，则从标准输入读入依赖关系
* `-n`：不执行Makefile中的命令而只输出命令
* `-s`：执行但不显示任何信息
### Make规则
默认情况下，make命令会在当前目录下寻找文件名为“Makefile”“makefile”“GNUmakefile”的文件
#### Makefile基本格式
```makefile{.line-numbers}
#规则语法1
targets: prequisites
    command
    ...

#规则语法2
target: prequisites; command
    command
    ...
```
参数表：
|参数|名称|备注|
| :--:| :--: | :---: |
|targets|目标文件|用空格分开，可以使用通配符|
|command|命令|与prequisites同行时用空格分开，不同行时开头用`\t`|
|prequisites|依赖目标|可以用`\`表示换行，但其后不能跟任何字符|
#### Makefile中的变量
Makefile中的变量是用一个字符串在Makefile中定义的，这个字符串就是变量的值
```makefile{.line-numbers}
#定义变量
VARNAME=string

#引用变量
    ${VARNAME}
```
除用户定义的变量外，make还允许使用环境变量、自动变量和预定义变量
常见的预定义变量：
|命令格式|含义|默认值|
| :---: | :---: | :---: |
|`AR`|库文件维护程序的名称|`ar`|
|`AS`|汇编程序名称|`as`|
|`CC`|C编译器名称|`cc`|
|`CPP`|C预编译器名称|`$(CC)-E`|
|`CXX`|C++编译器名称|`g++`|
|`RM`|文件删除程序的名称|`rm-f`|

常见的自动变量：
|命令格式|含义|
| :--: | :--: |
|`$*`|不包含扩展名的目标文件名称|
|`$+`|所有的依赖文件，以空格分开，并以出现的先后为序，可能包含重复的依赖文件|
|`$<`|第一个依赖文件的名称|
|`$?`|所有时间戳比目标文件晚的依赖文件，以空格分开|
|`$@`|目标文件的完整名称|
|`$^`|所有不重复的依赖文件，以空格分开|
|`$%`|如果目标是归档成员，则该变量表示目标的归档成员名称|

#### 引用其它makefile
* include前可以有一些空字符，但不能是`\t`开头
* include可以用一个或多个空格隔开文件
* make命令开始时，会寻找include所指出的其它makefile并安放在当前命令位置
* * 先在当前目录下寻找
* * 如果当前目录没找到，还会在以下几个目录找：
* * * 执行make时如果有参数`-I`或`--include-dir`，则在这个参数所制定的目录下寻找
* * * 如果目录/include（通常是/usr/local/bin或/usr/include）存在的话，也会去找
* 文件没找到会生成报警信息，但还会继续载入其它文件，一旦完成makefile读取，make会重试读取这些文件，如果还是不行才会出现致命信息
* 如果想要忽略无法读取的信息而继续执行，可以使用`-include <filename>`或`sinclude`
* 当环境中有环境变量MAKEFILES，这个环境变量也会被include进所有的makefile中
```makefile{.line-numbers}
include <filename> \#filename can be path
-include <filename>
sinclude <filename>

#引例
include foo.make *.mk  $(bar)
