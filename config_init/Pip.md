# Pip configuration

This note is written to set up pip.

---

## Installing pip

```bash
$ sudo apt install python3-pip
```

## Upgrading pip:

```bash
$ python3 -m pip install --upgrade pip

# Or this one:
$ pip install pip -U
```

## Changing the source for pip:

```bash
# Temporarily using ZJU Mirror to install [some-package]
$ pip install -i https://mirrors.zju.edu.cn/pypi/web/simple [some-package]

# Set ZJU Mirror as default source
$ pip config set global.index-url https://mirrors.zju.edu.cn/pypi/web/simple

# Upgrade pip using ZJU Mirror temporarily
$ pip install -i https://mirrors.zju.edu.cn/pypi/web/simple pip -U
```

> Check [ZJU Mirror](http://mirrors.zju.edu.cn/docs/pypi/) to see details.
