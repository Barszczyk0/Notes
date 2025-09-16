# Host validation bypass via connection state attack
# Objective
This lab is vulnerable to routing-based SSRF via the Host header. Although the front-end server may initially appear to perform robust validation of the Host header, it makes assumptions about all requests on a connection based on the first request it receives.

To solve the lab, exploit this behavior to access an internal admin panel located at `192.168.0.1/admin`, then delete the user `carlos`. 

# Solution
## Analysis
Access to admin panel is restricted (only available for local users).
|![](Images/image-26.png)|
|:--:| 
| *Access to admin panel is restricted* |


## Exploitation
### Verification of access to external and internal domains
Replacing original `Host` header value with Collabolator domain results in request to provided domain.

|![](Images/image-27.png)|
|:--:| 
| *Response from Collabolator* |

Replacing original `Host` header value with `192.168.0.1` results in `301 Moved Permanently`
|![](Images/image-28.png)|
|:--:| 
| *Modificattion of Host header value* |

### Sending 2 requests in single connection
Sending benign reqeust to `/` with `Connection: keep-alive` along with second request to `/admin` with header `Host: 192.168.0.1` allows attacker to access admin panel. Website performes thorough validation only on opening TCP connection request, therefore second request (reusing connection) gives attacker opportunity to access internal hosts.

|![](Images/image-29.png)|
|:--:| 
| *First request - standard requestt* |
|![](Images/image-31.png)|
| *Second requestt - request to admin panel - same connection* |
|![](Images/image-30.png)|
| *Second requestt - request to admin panel - same connection* |
|![](Images/image-32.png)|
| *Deletion of user carlos* |
