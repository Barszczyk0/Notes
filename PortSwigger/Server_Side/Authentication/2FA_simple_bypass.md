# 2FA simple bypass
# Objective
This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.
- Your credentials: wiener:peter
- Victim's credentials carlos:montoya
# Solution
In order to login user have to provide his username and password and then 2FA code. This code can be bypassed by jumping to: /my-account?id=carlos after /login .
|![](Images/image-4.png)|
|:--:| 
| *2FA Bypass* |