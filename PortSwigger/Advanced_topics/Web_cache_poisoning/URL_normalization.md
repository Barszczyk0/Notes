# URL normalization
# Objective
This lab contains an XSS vulnerability that is not directly exploitable due to browser URL-encoding. To solve the lab, take advantage of the cache's normalization process to exploit this vulnerability. Find the XSS vulnerability and inject a payload that will execute `alert(1)` in the victim's browser. Then, deliver the malicious URL to the victim. 

# Solution
## Analysis
Requests to static files, posts and non existing endpoints are cached.

|![](Images/image-44.png)|
|:--:| 
| *Normal request* |
|![](Images/image-45.png)|
| *Normal request to non existing endpoint* |

## Exploitation
Non existing endpoints allows to perform reflected XSS attack. Payload is in URl. By default browser URL encodes payload, therefore it does not execute. To bypass this attacker can use cache. In this case, cache key (URL) is normalized - when user makes request URL encoded request, cache normalizes URL and server attacker's payload.

|![](Images/image-46.png)|
|:--:| 
| *Cache poisoning with URL normalization* |
|![](Images/image-47.png)|
| *Browser request with XSS payload - browser encodes payload* |
|![](Images/image-48.png)|
| *Cache poisoning with URL normalization* |
|![](Images/image-49.png)|
| *Browser request with XSS payload - response served from cache after URL normalization* |
|![](Images/image-50.png)|
| *Browser request with XSS payload - response served from cache after URL normalization* |
