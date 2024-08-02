# Conda

---

## Installation

> 此处介绍的是在Linux下的安装操作

!!! info "官方信息"
    [anaconda.com](https://docs.anaconda.com/miniconda/)

### Download

首先在[清华源](https://mirrors.tuna.tsinghua.edu.cn/anaconda/)下载包

下载后得到文件`Miniconda3-latest-Linux-x86_64.sh`

### Install

使用Bash进行安装

```sh
bash Miniconda3-latest-Linux-x86_64.sh
```

安装完后进入Bash即可使用

## Configuration

### 加入Fish Shell

!!! note "配置信息"
    如果你也使用[Fish Shell](https://fishshell.com/)，那么可以参考这个配置

进入Bash，使用`conda init fish`将初始化命令加入fish中

### 修改prompt位置

如果要把`(base)`改到prompt左侧，在`~/.config/fish/config.fish`中加入

```sh
set -gx CONDA_LEFT_PROMPT 1
```

退出后重启终端即可

### 换源

换为清华源

```sh
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

---

## Usage

```sh
# 虚拟环境
conda create <--name|-n> <env_name>
conda create -n <env_name> python=3.8       # 创建虚拟环境
conda create -n <env_new> --clone <env_old> # 克隆虚拟环境
conda remove -n <env_name> --all
conda env remove -n <env_name>              # 删除虚拟环境
conda activate <env_name>                   # 激活虚拟环境
conda deactivate                            # 退出虚拟环境
conda create -n <env_new>
conda env list                              # 列出当前所有可用环境

# 软件包
conda install [-n <env_name>] <package_name>[=version] # 安装包[到指定环境中][版本号]
conda search <package_name>                            # 搜索软件包
conda list [-n <env_name>]                             # 列出[指定]环境中的所有包
conda update --all                                     # 更新所有已安装的软件包
conda remove [-n <env_name>] <package_name>            # 从环境中删除一个包

conda update conda             # 更新conda
```
