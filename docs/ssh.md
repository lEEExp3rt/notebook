# SSH 简明使用手册

有关SSH的简单使用手册

---

## Linux

### 安装SSH

首先查看本机是否安装了ssh：

```bash
dpkg -l | grep ssh
```

安装ssh客户端及服务端：

```bash
sudo apt-get install openssh-client
sudo apt-get install openssh-server
```

### 使用

查看是否已经启动SSH服务：

```bash
ps -e | grep ssh
```

启动服务：

```bash
sudo /etc/init.d/ssh <start | stop | restart>
sudo systemctl <start | stop | restart> ssh
```

远程连接：

```bash
ssh <username>@<IPaddress> [-X] [-p <port>]
# [-X]: 使用图形化界面
# [-p <port>]: 指定登录端口
```

### 密钥对

ssh生成一对公私钥，其中私钥保存在本机中，公钥可以分享以供连接

生成密钥：

```bash
ssh-keygen -t rsa 
```

拷贝公钥到远程主机：

```bash
ssh-copy-id <host>@<IPaddress>
```

公钥会保存在`~/.ssh/authorized_key`中

---

## Windows

以管理员身份登录Windows Powershell

```shell
net <start | stop | restart> sshd
```
