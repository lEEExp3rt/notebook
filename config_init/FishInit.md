# Fish Shell Configuraion

This note is written to install fish shell for Linux.

---

## Installation

```bash
$ sudo apt install fish
```

## Check the location:

```bash
$ which fish
```

## Change shell to fish as default

```bash
$ chsh -s /usr/bin/fish
```

## Change fish for root and users:

```bash
$ sudo vim /etc/passwd # root(in line 1) and user(in the last line)
```

## Fish themes

```bash
$ fish_config
```
