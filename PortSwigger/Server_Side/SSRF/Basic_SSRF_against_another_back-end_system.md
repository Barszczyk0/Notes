# Basic SSRF against another back-end system
# Objective
This lab has a stock check feature which fetches data from an internal system.\
\
To solve the lab, use the stock check functionality to scan the internal 192.168.0.X range for an admin interface on port 8080, then use it to delete the user carlos.

# Solution
## IP brute force
Website has `Check stock` functionality. In order to find correct admin interface last digit in IP address must be brute-forced.
|![](Images/image-6.png)|
|:--:| 
| *Modification of request* |
|![](Images/image-7.png)|
| *Payload position* |
|![](Images/image-8.png)|
| *Payload settings* |

The admin interface is at `192.168.0.95`
|![](Images/image-9.png)|
|:--:| 
| *Brute forced IP address* |

## SSRF Exploit
|![](Images/image-10.png)|
|:--:| 
| *URL to delete a username* |
|![](Images/image-11.png)|
| *Deletion of user carlos* |
