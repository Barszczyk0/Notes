# JWT authentication bypass via jku header injection
# Objective
This lab uses a JWT-based mechanism for handling sessions. The server supports the jku parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key. \
To solve the lab, forge a JWT that gives you access to the admin panel at `/admin`, then delete the user carlos.\
You can log in to your own account using the following credentials: `wiener:peter`
# Solution
## Analysis
The website in this lab uses JWT to handle different users.
|![](Images/image-31.png)|
|:--:| 
| *JWT* |

## Exploitation
### Injecting JKU header
```
JKU (JWK Set URL) - Provides URI that refers to a resource for a set of JSON public keys, one of which corresponds to the key that was used to sign the JWS.
```
