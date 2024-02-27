# MkDocs

使用MkDocs构建个人主页网站

> 参考教程：
>
> * [so easy！从头教你用mkdocs构建个人博客系统~_mkdocs教程-CSDN博客](https://blog.csdn.net/qq_41261251/article/details/116021097?ops_request_misc=%7B%22request%5Fid%22%3A%22170884087516800211528900%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170884087516800211528900&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-116021097-null-null.142^v99^pc_search_result_base7&utm_term=mkdocs&spm=1018.2226.3001.4187)

[TOC]

---

## Introduction

> *MkDocs* is a fast, simple and downright gorgeous static site generator that’s geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.

*MkDocs*是基于Markdown文档和YAML格式配置文件的快速静态站点生成器，主要用于构建项目文档

---

## Installation

### Windows

> :warning:需要Python3.5或Python3.6或Python3.7或Python3.8环境

```shell
$ pip install mkdocs
$ pip install mkdocs-material # Themes
```

使用如下命令查看是否安装完成：

```shell
$ mkdocs --version
```

显示版本号则安装成功，否则可以使用如下命令：

```shell
$ python3 -m mkdocs --version
```

将Python目录下的`Scripts`加入到环境变量`PATH`中即可实现上一条

### Debian Linux(Ubuntu)

```bash
$ sudo apt install mkdocs
```

使用以下命令查看是否安装完成：

```bash
$ mkdocs --version
```

---

## Usage

### 创建站点

```shell
$ mkdocs new <dir_name>
```

*MkDocs* 在当前目录下创建项目文件夹，包含`index.md`和`mkdocs.yml`

```shell
root@localhost ~ > mkdocs new Project
INFO    -  Creating project directory: Project
INFO    -  Writing config file: Project/mkdocs.yml
INFO    -  Writing initial docs: Project/docs/index.md

root@localhost ~ > cd Project

root@localhost ~/Project > tree
.
├── docs
│   └── index.md
└── mkdocs.yml

1 directory, 2 files
```

### 修改站点名

进入`mkdocs.yml`配置文件：

```yaml
site_name: <Your_Site_Name>
```

### 添加页面

*MkDocs*在初始化时为我们创建了初始页面`index.md`

进入`docs/`来添加页面

```shell
root@localhost:~/Project/docs > touch page2.md
```

然后进入`mkdocs.yml`并编辑：

```yaml
nav:
  - HOME: index.md
  - PAGE2: page2.md
```

并保存`mkdocs.yml`即可在浏览器实时查看添加的页面

#### 多级界面

也可以添加多级界面

```shell
root@localhost:~/Project/docs > mkdir page3
root@localhost:~/Project/docs > cd page3
root@localhost:~/Project/docs/page3 > touch page3-1.md
root@localhost:~/Project/docs/page3 > touch page3-2.md
root@localhost:~/Project/docs/page3 > mkdir page3-3
root@localhost:~/Project/docs/page3 > cd page3-3
root@localhost:~/Project/docs/page3/page3-3 > touch page3-3-1.md
root@localhost:~/Project/docs/page3/page3-3 > touch page3-3-2.md
root@localhost:~/Project/docs/page3/page3-3 > cd ~/Project
root@localhost:~/Project > tree
.
├── docs
│   ├── index.md
│   ├── page2.md
│   └── page3
│       ├── page3-1.md
│       ├── page3-2.md
│       └── page3-3
│           ├── page3-3-1.md
│           └── page3-3-2.md
└── mkdocs.yml

3 directories, 7 files
```

此时编辑`mkdocs.yml`：

```yaml
nav:
  - HOME: index.md
  - PAGE2: page2.md
  - PAGE3:
    - PAGE3-1: page3/page3-1.md
    - PAGE3-2: page3/page3-2.md
    - PAGE3-3:
      - page3-3-1: page3/page3-3/page3-3-1.md
      - page3-3-2: page3/page3-3/page3-3-2.md
```

即可查看多级页面

注意到添加页面都是使用***在`docs/`目录下***的绝对路径

> :warning:最多支持添加**3级**页面

### 站内跳转

在各界面的`.md`文档内使用链接方式进行站内跳转

```markdown
[AltText](RelativePath)
```

其中`RelativePath`为对应页面的`.md`文档与当前页面的相对路径

### 本地访问

进入项目文件夹

```shell
$ cd Project
$ mkdocs serve
```

打开浏览器，输入`http://127.0.0.1:8000`即可本地访问站点

在运行站点的同时，也可以修改站点信息，都可以实时在浏览器显示更改

### 远程部署

为了将网站部署到服务器上而不是仅限于本地浏览，使用以下命令：

```shell
$ mkdocs build
```

该命令将在项目目录下生成一个`site`目录，其中包含了静态站点的信息

#### GitHub部署

##### 项目站点

1. 用户`User`在GitHub上建立一个仓库`ProjectRepo`

2. 在项目目录下使用`git init`初始化和`git remote add`添加与远程仓库的连接

	```shell
	root@localhost:~/Project > git init
	root@localhost:~/Project > git remote add origin https://github.com/User/ProjectRepo.git
	```

3. 执行以下命令：

	```shell
	$ mkdocs gh-deploy
	```

	该命令会

	1. 创建远程分支`gh-pages`
	2. 将项目目录的`site/`推送到远程分支`gh-pages`
	3. 执行`mkdocs build`

4. 浏览器访问`http://User.github.io/ProjectRepo`即可查看

> :notebook: 通过把项目部署为一个站点，可以利用`master`分支上传源文档，用`gh-pages`分支上传`site/`下的文档

##### 个人页面

为了避免访问站点时在URL后填写项目名称的麻烦，可以使用个人页面的部署

1. 用户`User`在GitHub上建立仓库`User.github.io`

#### 云服务器

---

## Styles

### 图标

如果使用mkdocs主题，只需要在`docs/`目录下创建`img/`目录并放入图标文件`favicon.ico`

### 主题

*MkDocs*默认两个主题：`mkdocs`（默认）和`readthedoc`

修改配置文件`mkdocs.yml`：

```yaml
theme:
  name: <Your_Theme_Name>
```

也可以使用第三方主题，如[GitHub](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes)

