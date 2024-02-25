# File path traversal, traversal sequences blocked with absolute path bypass
# Objective
This lab contains a path traversal vulnerability in the display of product images.\
The application blocks traversal sequences but treats the supplied filename as being relative to a default working directory.\
To solve the lab, retrieve the contents of the `/etc/passwd` file.

# Solution
|![](Images/image-1.png)|
|:--:| 
| *Image location* |

|![](Images/image-2.png)|
|:--:| 
| *Retrieval of image using filename parameter* |

|![](Images/image-3.png)|
|:--:| 
| *Test of file traversal* |
|![](Images/image-4.png)|
| *Test of file traversal* |

Tests above showed that `/etc/passwd` is accessible but the content of the file couldn't be rendered corretly, but it worked via BurpSuite Repeater.

|![](Images/image-5.png)|
|:--:| 
| *Retrieval of `/etc/passwd`* |