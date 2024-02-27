# pwn shellcraft
```
List available payloads
pwn shellcraft -l
```
```
Generate shellcode which will spawn a shell with given euid
pwn shellcraft -f d amd64.linux.setreuid <euid>

Generate execve shellcode with"/bin///sh" and "['sh', '-p']" as parameters
pwn shellcraft i386.linux.execve "/bin///sh" "['sh', '-p']" -f a
```
