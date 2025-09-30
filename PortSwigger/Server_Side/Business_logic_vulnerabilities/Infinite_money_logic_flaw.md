# Infinite money logic flaw
# Objective
This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

# Solution
## Analysis
Initially application do not allow to buy item which price is above `Store credit`. Website has gift card functionality. Signing up for newsletter gives a customer coupon code `SIGNUP30`. Using this coupon gives user back `3$` as gift card.

|![](Images/image-40.png)|
|:--:|
| *Test of gift card functionality* |
|![](Images/image-41.png)|
| *Item is too expensive* |
|![](Images/image-42.png)|
| *Item is too expensive* |
|![](Images/image-43.png)|
| *Example purchase* |

## Exploitation
Using coupon code for buying gift card allows to gain `3$` with each transaction. To automate process of purchasing new gift cards with coupon code and applying new gift cards attacker can create a macro.

|![](Images/image-44.png)|
|:--:|
| *Macro configuration - configured requests* |
|![](Images/image-45.png)|
| *Macro configuration - deriving gift card value* |
|![](Images/image-46.png)|
| *Macro configuration - setting prvious gift card value* |
|![](Images/image-47.png)|
| *Macro configuration - testing* |
|![](Images/image-48.png)|
| *Session handling rules configurtion* |
|![](Images/image-49.png)|
| *Intruder configuration configurtion* |
|![](Images/image-50.png)|
| *Intruder configuration configurtion* |

