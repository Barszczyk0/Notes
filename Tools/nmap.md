# Nmap


# TCP Scans
## Connect Scan
```
nmap -sT <IP>

attacker (SYN) --> target
attacker <-- (SYN, ACK) target
attacker (ACK) --> target
Port is open
attacker (RST, ACK) --> target

attacker (SYN) --> target
attacker <-- (RST, ACK) target
Port is closed
```

## SYN Scan
```
nmap -sS <IP>

attacker (SYN) --> target
attacker <-- (SYN, ACK) target
Port is open
attacker (RST, ACK) --> target

attacker (SYN) --> target
attacker <-- (RST, ACK) target
Port is closed
```

## NULL Scan
```
nmap -sN <IP>

attacker () --> target
Port is open

attacker () --> target
attacker <-- (RST, ACK) target
Port is closed
```

## FIN Scan
```
nmap -sF <IP>

attacker (FIN) --> target
Port is open

attacker (FIN) --> target
attacker <-- (RST, ACK) target
Port is closed
```

## XMAS Scan
```
nmap -sX <IP>

attacker (FIN, PSH, URG) --> target
Port is open

attacker (FIN, PSH, URG) --> target
attacker <-- (RST, ACK) target
Port is closed
```

## Maimon Scan
```
nmap -sM <IP>

attacker (FIN, ACK) --> target
attacker <-- (RST) target
Port is open or closed
```

## ACK Scan
```
nmap -sA <IP>

attacker (ACK) --> target
attacker <-- (RST) target
Port is open or closed
```

## Window Scan
Similar to ACk SCAN. Window Scan examines the TCP Window field of the RST packets returned. On some systems, open ports use a positive window size (even for RST packets) while closed ones have a zero window.
```
nmap -sW <IP>

attacker (ACK) --> target
attacker <-- (RST) target
Port is open or closed
```

# UDP Scans
```
nmap -sU <IP>

attacker --> target
Port is open

attacker --> target
attacker <--(ICMP Type 3, Code 3) target
Port is closed
```

# ICMP Scan
## ICMP Echo Scan
```
nmap -PE -sn <IPs>

attacker (ICMP Echo Request) --> target
attacker <-- (ICMP Echo Reply) target
```

## ICMP Timestamp Scan
```
nmap -PP  -sn <IPs>

attacker (ICMP Timestamp Request) --> target
attacker <-- (ICMP Timestamp Reply) target
```

## ICMP Mask Scan
```
nmap -PP  -sn <IPs>

attacker (ICMP Address Mask Request) --> target
attacker <-- (ICMP  Address Mask Reply) target
```

# ARP Scan
```
nmap -PR -sn <IPs>
```

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

# Important
```
-sn - Skip port scan (host discovery only)
-Pn - Skip host discovery
```

# Misc
```
-T 4
-F
--top-ports 10
--min-rate <number>
--max-rate <number>
--min-parallelism <numprobes>
--max-parallelism <numprobes>
--badsum
--scanflags URG/ACK/PSH/RST/SYN/FIN
--ttl <NUMBER>
--script=vuln --script-args http.useragent="<USER AGENT>"
--spoof-mac <SPOOFED_MAC>
-D <IP1>,<IP2>,ME
```
