# Blind OS command injection with out-of-band interaction
# Objective
This lab contains a blind OS command injection vulnerability in the feedback function. \
\
The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain. \
\
To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator. 

# Solution

|![](Images/image-9.png)|
|:--:| 
| *Blind OS command injection with out-of-band interaction* |
