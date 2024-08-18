# Inconsistent security controls
# Objective
This lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees. To solve the lab, access the admin panel and delete the user `carlos`.

# Solution
## Analysis
Application possibly treats users from domain `@dontwannacry.com` differently than others.
|![](Images/image-9.png)|
|:--:| 
| *Item is too expensive* |
|![](Images/image-10.png)|
| *Registration confirmation email* |

## Exploitation
### Content discovery
```
$ gobuster dir -u https://0a89008c03d650b982397e6100250051.web-security-academy.net/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt\
...
/login                (Status: 200) [Size: 3393]
/register             (Status: 200) [Size: 3578]
/product              (Status: 400) [Size: 30]
/admin                (Status: 401) [Size: 2821]
...

```
|![](Images/image-11.png)|
|:--:| 
| *Access to admin panel is restricted* |

### Abuse of no new email confirmation
|![](Images/image-12.png)|
|:--:| 
| *Changed email* |
|![](Images/image-13.png)|
| *Access to admin panel* |