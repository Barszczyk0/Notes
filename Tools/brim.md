# Brim
## Queries
```
Communicated hosts
_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq

Frequently communicated hhosts
_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq -c | sort -r

Most active ports
_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count
_path=="conn" | cut id.orig_h, id.resp_h, id.resp_p, service | sort id.resp_p | uniq -c | sort -r 

Long connections
_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h, duration | sort -r duration

Transferred Data 
_path=="conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes

DNS and HTTP Queries
_path=="dns" | count () by query | sort -r
_path=="http" | count () by uri | sort -r

HTTTP connections
_path=="http" | cut id.orig_h, id.resp_h, id.resp_p, method, host, uri | uniq -c | sort value.uri

Suspicious Hostnames
_path=="dhcp" | cut host_name, domain

Suspicious IP Addresses
_path=="conn" | put classnet := network_of(id.resp_h) | cut classnet | count() by classnet | sort -r

Detect Files
filename!=null

SMB Activity
_path=="dce_rpc" OR _path=="smb_mapping" OR _path=="smb_files"

Threats
event_type=="alert" | count() by alert.severity,alert.category | sort count
```