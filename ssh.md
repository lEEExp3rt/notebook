# SSH

This note is written for ssh usage.

---

## Linux

### Check for package installation

```bash
$ dpkg -l | grep ssh
```

### Installation

```bash
$ sudo apt-get install openssh-client
$ sudo apt-get install openssh-server
```

### Check whether ssh-server is started

```bash
$ ps -e | grep ssh
```

### Start/Stop/Restart ssh

```bash
$ sudo /etc/init.d/ssh <option>

# or
$ sudo systemctl <option> ssh
```

### Log in

```bash
$ ssh <user>@<IPaddress> [-X] [-p <port>]
# [-X]: using GUI
# [-p <port>]: assigning <port> to log in
```

### Use public key to log in

```bash
$ ssh-keygen -t rsa 

# Copy the key to the remote host
$ ssh-copy-id <host@IPaddress>
```

> `ssh-copy-id` can only be used by Linux host and the public key will be written into `~/.ssh/authorized_key` in the remote host.

---

## Windows

Log in the Windows Powershell as administrator

```bash
$ net <option> sshd # <option>: start || stop || restart
```
