# Authentication bypass via information disclosure
# Objective
This lab's administration interface has an authentication bypass vulnerability, but it is impractical to exploit without knowledge of a custom HTTP header used by the front-end.\
\
To solve the lab, obtain the header name then use it to bypass the lab's authentication. Access the admin interface and delete the user carlos.\
\
You can log in to your own account using the following credentials: `wiener:peter`

# Solution
|![](Images/image-5.png)|
|:--:| 
| *Normal request* |
|![](Images/image-6.png)|
| *TRACE request - custom header with user IP* |
|![](Images/image-7.png)|
| *Adding new header to all requests* |
|![](Images/image-8.png)|
| *New option - Admin panel* |
|![](Images/image-9.png)|
| *Deleting user carlos* |