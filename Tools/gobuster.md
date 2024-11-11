# Gobuster
# Basics
```
-t          Set number of threads
-w          Use wordlist
-k          No TLS validation
--delay     Delay sending each packet
```

# Modes
## DIR Mode
```
gobuster dir -u "http://example.domain" -w wordlist.txt -x .php,.js
    -u  Target URL
    -w  Wordlist
    -x  Match extensions
    -r  Follow redirection
    -s  Match status codes
    -b  Filter out status codes
```

## DNS Mode
```
gobuster dns -d http://example.domain -w wordlist.txt
    -d  Target domain
    -r  Use custom DNS resolver
    -i  Show IPs that target domain resolve to
```

## VSHOT Mode
```
gobuster vhost -u "http://example.domain" -w wordlist.txt
gobuster vhost -u "http://127.0.0.1" --domain example.domain -w wordlist.txt --append-domain --exclude-length 100-300 
    -u  Target URL
    -w  Wordlist
    -r  Follow redirection
    -m  Method to use (GET/POST/...)
    --domain            Target domain
    --exclude-length    Filter out responses with specific length
    --append-domain     Use with '-d' for subdomain vhost enumeration
```