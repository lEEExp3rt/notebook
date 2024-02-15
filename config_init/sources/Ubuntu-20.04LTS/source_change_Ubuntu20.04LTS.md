# Apt Source Change For Ubuntu20.04LTS
## This note is written to change the apt source for Ubuntu20.04LTS<br>Written by lqy
---
### Source Code

*[ZJU](http://mirrors.zju.edu.cn/docs/ubuntu/)*:
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.zju.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.zju.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.zju.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.zju.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# 预发布软件源，不建议启用
# deb https://mirrors.zju.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

*[THU](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)*
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

---
### Steps
1. Back up:
```bash
sudo cp /etc/apt/sources.list sources.list.back
sudo cp sources.list.zju_Ubuntu20.04LTS /etc/apt #For example
sudo cp sources.list.thu_Ubuntu20.04LTS /etc/apt #For example
```

2. Change the source code:
```bash
sudo vim /etc/apt/sources.list
```

3. Update and upgrade:
```bash
sudo apt update 
```
