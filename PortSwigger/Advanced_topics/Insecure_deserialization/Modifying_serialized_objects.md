# Modifying serialized objects
# Objective
This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges. Then, delete the user `carlos`.
You can log in to your own account using the following credentials: `wiener:peter`

# Solution
## Analysis
The session cookie on this webiste holds serialized data:
|![](Images/image.png)|
|:--:| 
| *Session cookie* |

## Exploitation

|![](Images/image-1.png)|
|:--:| 
| *Modification of session cookie - 200 OK response* |
|![](Images/image-2.png)|
| *URL to delete carlos user* |
|![](Images/image-3.png)|
| *Deletion of user carlos* |