# SSH
# This note is written for ssh connection<br>Written by ***lqy***

---
### For OS Linux
1. First check whether ssh client and server are installed or not:
```bash
dpkg -l | grep ssh
```

2. Install:
```bash
sudo apt-get install openssh-client
sudo apt-get install openssh-server
```

3. Check whether ssh-server is started:
```bash
ps -e | grep ssh
```

4. Start/Stop/Restart ssh:
```bash
sudo /etc/init.d/ssh [option]
#or
sudo systemctl [option] ssh
```

5. Log in:
```bash
ssh user@IPaddress

#Using GUI:
ssh -X user@IPaddress

#Changing port:
ssh -p port user@IPaddress
```

6. Use public key to log in:
```bash
ssh-keygen -t rsa 
#-t means choosing type, and RSA is adopted, and passphrase can be empty

#copy the key to the remote host:
ssh-copy-id host@IPaddress
#This step can only be used by Linux host and the public key will be written into ~/.ssh/authorized_key in the remote host.
```

---
### For Windows:
log in the Windows Powershell in administrator
```bash
net [option] sshd
#option can be start,stop and restart
```
