# Limit overrun race conditions
# Objective
This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.\
To solve the lab, successfully purchase a Lightweight L33t Leather Jacket.\
You can log in to your account with the following credentials: `wiener:peter`. 

# Solution
## Analysis
Application do not allow to buy item which price is above `Store credit`.
|![](Images/image.png)|
|:--:| 
| *There is a discount code available on the website* |
|![](Images/image-1.png)|
| *Checkout* |
|![](Images/image-2.png)|
| *Request with discount code* |
|![](Images/image-3.png)|
| *Duplicated request with discount code* |

## Exploitation
### Exploiting race conditions
In order to reduce price attacker can try to exploit race conditions by sending `POST /cart/coupon` request in parallel (making use of the same  discount code multiple times).

|![](Images/image-4.png)|
|:--:| 
| *Creating tab group* |
|![](Images/image-5.png)|
| *Dublicating tab (request) to 25 tabs (requests)* |
|![](Images/image-6.png)|
| *Modifying send method - Send group in parallel* |
|![](Images/image-7.png)|
| *Result* |
|![](Images/image-8.png)|
| *Result* |
