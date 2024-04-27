# Ffuf

## Username and password brute force
```
ffuf -request request.txt -mode clusterbomb -w usernames.txt:USERFUZZ -w passwords.txt:PASSFUZZ -fs 1234
```

## Directory enumeration
```
ffuf -u "http://$ip/FUZZ" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -fw 14867
```

## Subdomain enumberation
```
ffuf -u http://$ip -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words.txt -H "Host: FUZZ.creative.thm" -fw 6
```
