# Zeek

## Zeek
Read file and ignore checksums:
```
zeek -C -r sample.pcap
```

## Zeek-cut
Previous command woud create `.log` files. Those files can be read and filtered using `zeek-cut`:
```
cat sample.log | zeek-cut uid proto id.orig_h id.orig_p
```

## Zeek signatures
Read file, ignore checksums match for signatures:
```
zeek -Cr sample.pcap -s demo.sig
```
### Example signature files
Cleart text http password detection - `http_password.sig`:
```
signature http-password {
    ip-proto == tcp
    dst-port == 80
    payload /.*password.*/
    event "Cleartext Password Found!"
}
```

Ftp password brute-force detection - `ftp_brute.sig`:
```
signature ftp-brute {
    ip-proto == tcp
    payload /.*530.*Login.*incorrect.*/
    event "FTP Brute-force Attempt"
}
```

## Zeek scripting
Launch `zeek` with script `demo.zeek` that would be performed on `sample.pcap`:
```
zeek -Cr sample.pcap demo.zeek 
```

Load local scripts (`/opt/zeek/share/zeek/base`) to your current working directory:
```
zeek -Cr sample.pcap local 
```

Load specific scripts:
```
zeek -Cr sample.pcap /opt/zeek/share/zeek/policy/protocols/ftp/detect-bruteforcing.zeek 
```

Scripts locations:
```
/opt/zeek/share/zeek/base
/opt/zeek/share/zeek/site
/opt/zeek/share/zeek/policy
/opt/zeek/share/zeek/site/local.zeek
```

Custom scripts locations:
```
/opt/zeek/share/zeek/base/bif
/opt/zeek/share/zeek/base/bif/plugins
/opt/zeek/share/zeek/base/protocols
```

### Example scripts
New connections (basic):
```
event new_connection(c: connection)
{
	print c;
}
```

New connections (print connection direction):
```
event new_connection(c: connection)
{
	print ("###########################################################");
	print ("");
	print ("New Connection Found!");
	print ("");
	print fmt ("Source Host: %s # %s --->", c$id$orig_h, c$id$orig_p);
	print fmt ("Destination Host: resp: %s # %s <---", c$id$resp_h, c$id$resp_p);
	print ("");
}

# %s: Identifies string output for the source.
# c$id: Source reference field for the identifier.
```

Combining scripts and signatures:
```
event signature_match (state: signature_state, msg: string, data: string)
{
if (state$sig_id == "demo_signature")
    {
    print ("Signature hit! --> #DEMO_SIGNATURE");
    }
}
```

## Zeek frameworks
Zeek frameworks can be loaded from script file or called directly.
```
zeek -Cr sample.pcap /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek 
zeek -Cr sample.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
zeek -Cr sample.pcap intelligence-demo.zeek 
zeek -Cr sample.pcap hash-demo.zeek
```

Contents of `intelligence-demo.zeek`:
```
# Load intelligence framework!
@load /opt/zeek/share/zeek/policy/frameworks/intel/seen
@load /opt/zeek/share/zeek/policy/frameworks/intel/do_notice.zeek
redef Intel::read_files += { "/opt/zeek/intel/zeek_intel.txt" };
```

Contents of `hash-demo.zeek` - alternative way of loading scripts: 
```
# Enable MD5, SHA1 and SHA256 hashing for all files.
@load /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
```

## Zeek package manager - zkg
### Commands
```
zkg install package_path/git_url
zkg list
zkg remove
zkg upgrade
```

Useful modules:
```
zeek -Cr sample.pcap zeek-sniffpass
zeek -Cr sample.pcap geoip-conn
```

Ways of callinng a module:
```
zeek -Cr sample.pcap sniff-loading-script.zeek 
zeek -Cr sample.pcap /opt/zeek/share/zeek/site/zeek-sniffpass
zeek -Cr sample.pcap zeek-sniffpass 
```