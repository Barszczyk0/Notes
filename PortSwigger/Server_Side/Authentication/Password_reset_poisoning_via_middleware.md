# Password reset poisoning via middleware
# Objective
This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives. 

To solve the lab, log in to Carlos's account. You can log in to your own account using the following credentials: `wiener:peter`. Any emails sent to this account can be read via the email client on the exploit server. 

# Solution
## Analysis
|![](Images/image-50.png)|
|:--:| 
| *Reseting password funcionality* |
|![](Images/image-51.png)|
| *Password reset link sent to user via email* |
|![](Images/image-52.png)|
| *Setting new password* |

## Exploitation
Using `X-Forwarded-Host` attacker can create forgot password link with other domain. When victim's tries to open the link, attacker will have access to victim's reset password token.

|![](Images/image-53.png)|
|:--:| 
| *Password reset poisoning* |
|![](Images/image-54.png)|
| *Reset password link with attacker's domain* |

|![](Images/image-55.png)|
|:--:| 
| *Reseting victim's password* |
|![](Images/image-56.png)|
| *Victim request to attacker domain with password reset token* |
|![](Images/image-57.png)|
| *Reseting victim's password* |
