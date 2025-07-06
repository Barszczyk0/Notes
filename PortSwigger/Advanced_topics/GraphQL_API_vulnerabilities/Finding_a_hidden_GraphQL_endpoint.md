# Finding a hidden GraphQL endpoint
# Objective
The user management functions for this lab are powered by a hidden GraphQL endpoint. You won't be able to find this endpoint by simply clicking pages in the site. The endpoint also has some defenses against introspection.

To solve the lab, find the hidden endpoint and delete `carlos`. 

# Solution
## Analysis
Website uses GraphQL to manage informations about posts and users.

|![](Images/image-10.png)|
|:--:| 
| *Hidden GraphQL endpoint* |

## Exploitation
### Running introspection query
After adding `\n` after `__schema` website allows for introspection query, which discloses information about database structure as well as hidden fields and functions. Not every available function from introspection query result was visible in visualization below.

|![](Images/image-12.png)|
|:--:| 
| *Introspection query - Introspection is not allowed* |
|![](Images/image-11.png)|
| *Introspection query - Filter Bypass - Modification of default instrospcetion query* |
|![](Images/image-13.png)|
| *Introspection query - Visualization of introspection results* |
|![](Images/image-14.png)|
| *ID of user Carlos - ID 3* |
|![](Images/image-15.png)|
| *Deletion of user Carlos by ID* |


