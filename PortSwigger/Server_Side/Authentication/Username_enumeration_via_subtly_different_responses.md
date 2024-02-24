# Username enumeration via subtly different responses
# Objective
This lab is subtly vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:
- [username.txt](https://portswigger.net/web-security/authentication/auth-lab-usernames) 
- [passwords.txt](https://portswigger.net/web-security/authentication/auth-lab-passwords) 

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

# Solution
## Username Enumeration
|![](Images/image-8.png)|
|:--:| 
| *Payload position* |
|![](Images/image-9.png)|
| *Grep-Extract setings* |
|![](Images/image-10.png)|
| *Different respose - no full stop at the end* |

Valid username is academico

## Password brute-force
|![](Images/image-11.png)|
|:--:| 
| *Payload position* |
|![](Images/image-12.png)|
| *Brute-forced password - maggie* |