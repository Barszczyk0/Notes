# Weak isolation on dual-use endpoint
# Objective
This lab makes a flawed assumption about the user's privilege level based on their input. As a result, you can exploit the logic of its account management features to gain access to arbitrary users' accounts. To solve the lab, access the `administrator` account and delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter`

# Solution
## Analysis
The website has `Change Password` functionality.

|![](Images/image-31.png)|
|:--:| 
| *Test of change password functionality* |


## Exploitation
Absence of `current-password` value in `Change Password` requests results in valid requests.

|![](Images/image-32.png)|
|:--:| 
| *Change password request without old password* |
|![](Images/image-33.png)|
| *Changing administrator password* |
|![](Images/image-34.png)|
| *Deletion of user Carlos* |
