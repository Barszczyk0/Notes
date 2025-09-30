# Authentication bypass via encryption oracle
# Objective
This lab contains a logic flaw that exposes an encryption oracle to users. To solve the lab, exploit this flaw to gain access to the admin panel and delete the user carlos.

You can log in to your own account using the following credentials: `wiener:peter`

# Solution
## Analysis
The website has `Stay logged in` functionality.

|![](Images/image-51.png)|
|:--:| 
| *Stay logged in functionality* |

When user provides invalid email address, there is a error information using encrypted `notification` cookie.
|![](Images/image-52.png)|
|:--:| 
| *Invalid email address* |

## Exploitation
To display information about invalid email, website decrypts value from `notification` cookie. This cookie can be used to decrypt the value of `stay-logged-in` cookie. 

To dencrypt any data attacker can use `POST /post/comment` request.
|![](Images/image-53.png)|
|:--:| 
| *Decrypting data* |

To encrypt any data attacker can use `GET /post?postId=9` request with `notification` cookie.
|![](Images/image-54.png)|
|:--:| 
| *Encrypting data* |

Knowing the structure of `stay-logged-in` cookie attacker can attempt to forge it. To do this successfully string: `Invalid email address: ` must be stripped.



Original value:
```
wiener:1759255788916
```

Target value:
```
administrator:1759255788916
```

In order to skip 23 bytes string `Invalid email address: `, the payload must be padded with 9 bytes (letters). Then first 32 (23+9) bytes must be cut out.

|![](Images/image-55.png)|
|:--:| 
| *Input length error* |

|![](Images/image-57.png)|
|:--:| 
| *Encrypting new cookie value* |
|![](Images/image-56.png)|
| *Cookie modification - deleting first 32 bytes using regex `^([0-9a-f]{2}\s){32}`* |
|![](Images/image-58.png)|
| *Cookie modification - encoding cookie* |
|![](Images/image-59.png)|
| *Cookie verification* |
|![](Images/image-60.png)|
| *Using forged cookie* |
|![](Images/image-61.png)|
| *Deletion of user Carlos* |
