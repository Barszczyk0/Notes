# Reflected XSS into HTML context with nothing encoded
# Objective
This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.\
\
To solve the lab, perform a cross-site scripting attack that calls the alert function.

# Solution
The following payload triggers `alert()`:
```
<script>alert()</script>
```