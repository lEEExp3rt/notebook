# Fish Shell Configuraion
## This note is written to install fish shell for Linux<br>Written by ***lqy***
---

1. Fish installation:
```bash
sudo apt install fish
```

2. Check the location:
```bash
which fish
```

3. Change shell to fish as default
```bash
chsh -s /usr/bin/fish
```

4. Change fish for root and users:
```bash
sudo vim /etc/passwd #root(in line 1) and user(in the last line)
```

5. Fish themes:
```bash
fish_config
```
