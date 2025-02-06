# JWT authentication bypass via algorithm confusion

# Objective
This lab uses a JWT-based mechanism for handling sessions. It uses a robust RSA key pair to sign and verify tokens. However, due to implementation flaws, this mechanism is vulnerable to algorithm confusion attacks.

To solve the lab, first obtain the server's public key. This is exposed via a standard endpoint. Use this key to sign a modified session token that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter`

# Solution
## Analysis

On the website there is `/jwks.json` file accesible.

|![](Images/image-44.png)|
|:--:| 
| *Public key* |

## Exploitation
### Explaination of algorithm confusion attack
The idea behind of algorithm confusion is that in certain circumstances (bad implementan) public key may be treated by server as symmetric key. Attacker can bypass token validation by: modifying algorithm filed to symmetric algorithm, taking public key and using it to sign JWT token.

Full explaination - [PortSwigger](https://portswigger.net/web-security/jwt/algorithm-confusion).
```js
function verify(token, secretOrPublicKey){
    algorithm = token.getAlgHeader();
    if(algorithm == "RS256"){
        // Use the provided key as an RSA public key
    } else if (algorithm == "HS256"){
        // Use the provided key as an HMAC secret key
    }
}
```

```python
publicKey = <public-key-of-server>;
token = request.getCookie("session");

# Devolopers assumed that it will exclusively handle JWTs signed using an asymmetric algorithm
# In case of symmtric algorithm set in JWT, public key will be treated as symmetric key
verify(token, publicKey);
```

### Performing an algorithm confusion attack
In order to exploit algorithm confusion attacker has to:
1. Obtain the server's public key
2. Convert the public key to a suitable format
3. Create a malicious JWT with a modified payload and the alg header set to HS256.
4. Sign the token with HS256, using the public key as the secret. 

Obtained public keys:
```json
{
    "kty":"RSA",
    "e":"AQAB",
    "use":"sig",
    "kid":"90580691-9aeb-41c7-813e-e6ee4352b798",
    "alg":"RS256","n":"oQVeLj52qKW-eG2HMd5iVeO8TU8iJmcHLmnvzWVFsyDt1LybFqjCcFI8BeorylnltWQSX12TZMKJYv8EFdUZOPDMwGDJCte0jUAoqLJBgoI3vDdbvJY7InalR1fhr9UQnQQf_y4maOxvMX39vY6DO2xAPk4FZyEajp1gWPMkYZWedQMIh10VRk7d53kU-cZJAQ7Fxbz7bFYptkI3Hq8_PVuJDyaRWNPJlbhTmUMibEe9ErB_JviPptwmOFeo4BcHSVU-h8gpNvqMoI3KwBv_yF2nT4_GSvUr77mFSg_kZb27fzG4UvmjVntvW0d2nrhzHBLHcNihGZC4lD8M06ufzQ"
}
```

|![](Images/image-45.png)|
|:--:| 
| *Creation of Public key using obtained earlier public key* |
|![](Images/image-46.png)|
| *Copying created public key as PEM* |
|![](Images/image-47.png)|
| *Base64 encoding PEM public key* |
|![](Images/image-48.png)|
| *Creating symmetric key from Base64 encoded public key - Modification of the k value (key size does not matter)* |
|![](Images/image-49.png)|
| *Modification and signing JWT token using created symmetric key* |
|![](Images/image-49.png)|
| *Deletion of user carlos* |


