# nmap
# Changing source port for scanning
```
nmap -sS -g <PORT_NUMBER> <IP>
nmap -sS --source-port <PORT_NUMBER> <IP>
```

# Packet fragmentation
```
-f    - to set the data in the IP packet to 8 bytes
-ff   - to limit the data in the IP packet to 16 bytes at most
--mtu SIZE - to provide a custom size for data carried within the IP packet (multiples of 8)
```

# Misc
```
--badsum
--scanflags URG/ACK/PSH/RST/SYN/FIN
--ttl <NUMBER>
```
