# Accidental exposure of private GraphQL fields
# Objective
The user management functions for this lab are powered by a GraphQL endpoint. The lab contains an access control vulnerability whereby you can induce the API to reveal user credential fields.

To solve the lab, sign in as the administrator and delete the username `carlos`. 

# Solution
## Analysis
Website uses GraphQL to retrieve informations about posts.

|![](Images/image-6.png)|
|:--:| 
| *GraphQL example query* |

## Exploitation
### Running introspection query
Website allows for introspection query, which discloses information about database structure as well as hidden fields and functions.

|![](Images/image-7.png)|
|:--:| 
| *Introspection query - password field* |
|![](Images/image-5.png)|
| *Introspection query - Visualization of introspection results* |
|![](Images/image-8.png)|
| *Retrieaval of password field from administrator (id:1)* |
|![](Images/image-9.png)|
| *Retrieaval of password field from administrator (id:1)* |


