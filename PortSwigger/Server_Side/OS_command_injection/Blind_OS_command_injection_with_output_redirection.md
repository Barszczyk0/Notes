# Blind OS command injection with output redirection
# Objective
This lab contains a blind OS command injection vulnerability in the feedback function.\
The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at: `/var/www/images/` \
The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file. \
To solve the lab, execute the whoami command and retrieve the output.

# Solution
|![](Images/image-6.png)|
|:--:| 
| *Redirecting OS command injection output to a file* |

|![](Images/image-7.png)|
|:--:| 
| *Image location* |

|![](Images/image-8.png)|
|:--:| 
| *Requesting created earlier file with OS command injection output* |