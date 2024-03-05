# Basic SSRF against the local server
# Objective
This lab has a stock check feature which fetches data from an internal system.\
\
To solve the lab, change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user carlos.

# Solution
## Analysis
By changing `stockAPI` value it is possible to reach `/admin` page.

|![](Images/image.png)|
|:--:| 
| *Original stockAPI URL* |
|![](Images/image-1.png)|
| *Modification of stockAPI value* |

|![](Images/image-2.png)|
|:--:| 
| *Normal behaviour* |
|![](Images/image-3.png)|
| *SSRF* |

## Deletion of user carlos
User carlos must be deleted using the technique above. Admin page cannot be accessed from outside.
|![](Images/image-4.png)|
|:--:| 
| *Error* |
|![](Images/image-5.png)|
| *Deletion of user carlos* |
