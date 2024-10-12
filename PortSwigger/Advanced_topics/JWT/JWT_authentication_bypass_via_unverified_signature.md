# JWT authentication bypass via unverified signature
# Objective
This lab uses a JWT-based mechanism for handling sessions. Due to implementation flaws, the server doesn't verify the signature of any JWTs that it receives.\
To solve the lab, modify your session token to gain access to the admin panel at `/admin`, then delete the user `carlos`.\
You can log in to your own account using the following credentials: `wiener:peter`

# Solution
## JWT Editor
Working with JWT can be easier thanks to extension called `JWT Editor`:

|![](Images/image.png)|
|:--:| 
| *Extension for working with JWT - JWT Editor* |
|![](Images/image-1.png)|
| *Packets with JWT tokens are marked green* |

## Analysis
The website in this lab uses JWT to handle different users. If JWT signature is not checked on the server, client (attacker) can modify base64 encoded JWT to impersonate administrator:

|![](Images/image-3.png)|
|:--:| 
| *Admin Panel* |
|![](Images/image-2.png)|
| *JWT contents* |

There is `/admin` endpoint that returns `HTTP 401 Unauthorized`.

## Exploitation

|![](Images/image-4.png)|
|:--:| 
| *Modification of JWT* |
|![](Images/image-5.png)|
| *Original request* |
|![](Images/image-6.png)|
| *Modified request - changed URL and JWT token* |
|![](Images/image-7.png)|
| *Access to admin panel - URL to delete carlos user* |
|![](Images/image-8.png)|
| *JWT substituion and deletion of user carlos* |