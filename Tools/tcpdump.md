# Tcpdump
## Basics
```
tcpdump -i any -c 5 -n
    -i  Interface
    -c  Number of packets to capture
    -n  Don’t resolve IP addresses
    -nn Don’t resolve IP addresses and don’t resolve port numbers
    -q  Quick information 
    -A  Show packet data in ASCII
    -e  Display data link layer headers information

    -r  Read .pcap from file
    -w  Write .pcap to file
```

# Filtering
## Filtering by host

```
tcpdump -i any -n host "<domain>"
tcpdump -i any -n src host "<IP>"
```

## Filtering by port

```
tcpdump -i any -n port 80
```

## Filtering by protocol

```
tcpdump -i any -n "<ip/ipv6/icmp/tcp/udp/icmp>"
```

## Logical operators

```
and/or/not - Normal
&/|/!      - Bitwise
```

## Filtering based on header values

```
ether[0] & 1 != 0
    # Catch all multicast packets
```

```
tcpdump "tcp[tcpflags] == tcp-syn"
    # Catch TCP packets with only SYN flag set
tcpdump "tcp[tcpflags] & tcp-syn != 0"
    # Catch TCP packets with at least SYN flag set
```

