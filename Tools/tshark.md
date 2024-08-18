# Tshark
## Basics
List available sniffing interfaces:
```
tshark -D
```
Capture traffic on a interface:
```
tshark -i eth0
```

Write output to file / Read data from file
```
tshark -w output_file.pcap
tshark -r inputt_file.pcap
```

Modes:
```
-s      Silent
-V      Verbose
-x      Hex
```

Capture conditions
```
tshark -a       -->     Autostop condition
tshark -b       -->     Infinite loop
```

## Useful options
```
-c $n                   -->     Show first `n` packets
--color                 -->     Color output like in wireshark
-T fields -e <field_name>        -->     Extract specified fields from pcap
```

## Statistics
```
-z io,phs -q            -->     Show protocol hierarchy
-z endpoints,ip -q      -->     Endpoints statistics
-z conv,ip -q`          -->     IP conversations
-z ip_hosts,tree -q     -->     IP hosts statistics
-z ip_srcdst,tree -q    -->     IP src/dst statistics
-z dns,tree -q          -->     DNS statistics
-z credentials -q       -->     Credentials

-z follow,<udp/tcp/http>,ascii,<strem_number> -q    -->     Follow stream
```


## Capture filters
```
Captture FFFilters  -->  -f

tshark -f "host 10.0.0.1"
tshark -f "net 10.0.0.0/16"
tshark -f "src host 10.0.0.1"
tshark -f "dst host 10.0.0.2"

tshark -f "port 69"
tshark -f "portrange 10-200"

tshark -f "tcp"
tshark -f "http"
```

## Display Filters
```
DisplaYYY Filters   -->  -Y

tshark -Y 'ip.addr == 10.0.0.1'
tshark -Y 'ip.addr == 10.0.0.0/16'
tshark -Y 'ip.src == 10.0.0.1'
tshark -Y 'ip.dst == 10.0.0.2'

tshark -Y 'tcp.port == 69'
tshark -Y 'tcp.port >= 10 and tcp.port <= 200'

tshark -Y 'tcp'
tshark -Y 'http'
```

## Practical examples

```
Get all domains from based on dns traffic:
tshark -r demo.pcap -Y "dns.count.answers > 0" -T fields -e dns.qry.name -e dns.resp.name

Show IP addresses based on dns responses:
tshark -r demo.pcap -Y "dns.flags.response == 1" -T fields -e dns.qry.name -e dns.a

Show all http requests sent to given domain:
tshark -r demo.pcap -Y 'http.host == "example.com" || http.host == "anotherexample.com"' -T fields -e frame.number -e ip.src -e http.host -e http.request.uri

Show server information based on http responses:
tshark -r demo.pcap -Y 'http.response' -T fields -e frame.number -e ip.src -e ip.dst -e http.host -e http.server

Exporting all http/smb/tftp objects:
tshark -r demo.pcap --export-objects http,http_export_directory
tshark -r demo.pcap --export-objects smb,smb_export_directory
tshark -r demo.pcap --export-objects tftp,tftp_export_directory
```

