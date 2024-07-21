# Web cache poisoning via an unkeyed query string
# Objecttive
This lab is vulnerable to web cache poisoning because the query string is unkeyed. A user regularly visits this site's home page using Chrome. To solve the lab, poison the home page with a response that executes `alert(1)` in the victim's browser.

# Solution
## Analysis
|![](Images/image-28.png)|
|:--:| 
| *Normal request* |
|![](Images/image-29.png)|
| *Request with extra parameter* |
|![](Images/image-30.png)|
| *Response to request with extra parameter is cached* |
|![](Images/image-31.png)|
| *Response to request with modified extra parameter comes still from cache* |
|![](Images/image-32.png)|
| *Response to request with modified extra parameter comes still from cache* |

## Exploitation
Payload:
```
GET /?xyz=xyz'/><script>alert(1)</script>
```

|![](Images/image-33.png)|
|:--:| 
| *Web cache poisoning (for Chrome's User-Agent)* |