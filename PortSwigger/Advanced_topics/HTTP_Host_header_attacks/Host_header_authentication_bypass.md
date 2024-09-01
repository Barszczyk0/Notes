# Host header authentication bypass
# Objective
 This lab makes an assumption about the privilege level of the user based on the HTTP Host header.

To solve the lab, access the admin panel and delete the user carlos. 

# Solution
## Analysis
There is a admin panel at `/admin`. Access to it is restricted (only available for local users). This directory appears in `robots.txt`.
|![](Images/image-4.png)|
|:--:| 
| *Access to admin panel is restricted* |
|![](Images/image-5.png)|
| *Access to admin panel is restricted* |


## Exploitation
|![](Images/image-6.png)|
|:--:| 
| *Host header modification* |
|![](Images/image-7.png)|
| *URL to delete a user* |
|![](Images/image-8.png)|
| *Deletion of user carlos* |
