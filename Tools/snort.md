# Snort 
```
sudo snort -c /etc/snort/snort.conf -T -q
    -c configuration
    -T snort's self-test 
    -q quiet
```

# Sniffer mode
```
sudo snort -v -i eth0
    -v verbose mode
    -i interface
```

```
sudo snort -d -e
    -d display the packet data
    -e display the link-layer 
```

```
sudo snort -X
    -X display the full packet details in HE
```

# Logger mode
```
snort -dev -l .
    -dev
    -l create log files in specified directory
```

```
sudo snort -dev -K ASCII
    -dev
    -K log packets in ASCII format
```

# Reading files
## Reading generated logs
```
sudo snort -dvr snort.log.5678459890 -n 10
    -d dispaly the packet data
    -v verbose mode
    -r read snort log file
    -n read first 10 packets
```

## Reading pcap file
```
sudo snort -r icmp-test.pcap
sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console
sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp.pcap http.pcap" -A console 
```

## Filtering
```
sudo snort -r snort.log.5678459890 icmp
sudo snort -r snort.log.5678459890 udp
sudo snort -r snort.log.5678459890 'udp and port 53'
```

## IDS/IPS mode
```
sudo snort -c /etc/snort/snort.conf -T
    -c configuration (IDS/IPS alerts, messages, etc.)
    -T snort's self-test 
```


```
sudo snort -c /etc/snort/snort.conf -N -D
    -c configuration
    -N disable loggging
    -D background mode
```


```
sudo snort -c /etc/snort/snort.conf -A full
    -A alert mode (console/cmg/full/fast/none)
```


```
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A cmg
    -c configuration
    -q quiet
    -Q --daq IPS mode
    -i interface 
    -A alert mode
```