# GDB Plugins configuraion

This note is written for gdb plugins configurations.

---

## Installation

```bash
$ git clone https://github.com/gatieme/GdbPlugins.git ~/GdbPlugins #Get the plugin files
```

## Configuration

```bash
$ echo "source ~/GdbPlugins/peda/peda.py" > ~/.gdbinit 
$ echo "source ~/GdbPlugins/gef/gef.py" > ~/.gdbinit 
$ echo "source ~/GdbPlugins/gdbinit/gdbinit" > ~/.gdbinit
```
