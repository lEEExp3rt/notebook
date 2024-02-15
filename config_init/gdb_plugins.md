# GDB Plugins configuraion
## This note is written to install gdb plugins<br>Written by ***lqy***
---

1. Install plugins:
```bash
git clone https://github.com/gatieme/GdbPlugins.git ~/GdbPlugins #Get the plugin files
```

2. Start the plugins:
```bash
echo "source ~/GdbPlugins/peda/peda.py" > ~/.gdbinit 
echo "source ~/GdbPlugins/gef/gef.py" > ~/.gdbinit 
echo "source ~/GdbPlugins/gdbinit/gdbinit" > ~/.gdbinit
```
