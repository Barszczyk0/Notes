# Brute-forcing a stay-logged-in cookie
# Objective
This lab allows users to stay logged in even after they close their browser session. The cookie used to provide this functionality is vulnerable to brute-forcing. To solve the lab, brute-force Carlos's cookie to gain access to his "My account" page.

Your credentials: `wiener:peter`\
Victim's username: `carlos`\
[Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

# Solution
## Analysis
|![](Images/image-37.png)|
|:--:| 
| `stay-logged-in` cookie value |
|![](Images/image-38.png)|
| `stay-logged-in` cookie construction |

Cookie construction:
```
base64(username+':'+md5(user_password))
```

## Exploitation
|![](Images/image-39.png)|
|:--:| 
| *Preparation of brute force list* |
|![](Images/image-40.png)|
| *Payload position* |
|![](Images/image-41.png)|
| *Payload modifications using Burp Suite payload processing* |
|![](Images/image-42.png)|
| *Brute force result* |
