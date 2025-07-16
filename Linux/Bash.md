# Bash
## Important bash information
### Terminal Shorcuts
```
alt-f  - go forward word
alt-b  - go backwards word

ctrl-f - go forward char
ctrl-b - go backwards char

alt-t  - swap words
ctrl-t - swap char

ctrl-w - delete one word backwards
alt-d  - delete one word forwards
ctrl-u - delete entire line to left

ctrl-a - go to the start of the line
ctrl-e - go to the end of the line

ctrl-r - reverse search
```

## Commands - Enumeration
### List of users and privileges
```
sudo -l
ls /home
cat /etc/passwd | grep -v '/nologin' | cut -d: -f1
```

### Environment variables
```
env 
echo $PATH
```

### Searching interesting/valuable files/information
```
getcap -r / 2>/dev/null
find / -perm -4000 -type f 2>/dev/null
find / \( -user root -o -user ubuntu \) 2>/dev/null
find / -type f \( -name "*pass*" -o -name "*key*" -o -name "*.conf" \) 2>/dev/null
grep -r "." /etc/cron* 2>/dev/null
```

### Checking open/listening ports
```
ss -tulpn
ps -eo pid,cmd --sort=-%mem | grep -v grep | while read pid cmd; do lsof -p $pid 2>/dev/null | grep -q 'IPv4' && echo "$pid $cmd"; done
```
