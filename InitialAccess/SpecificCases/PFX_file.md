## PFX file
Crack the password with John first.
```
# Generate text file john understands
pfx2john file.pfx > hash.txt

# Crack the output file
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
With the password, I can extract the key and certificate. 
When extracting the key, it asks for the password, and then a password for the output .pem file:
```
openssl pkcs12 -in file.pfx -nocerts -out file.key-enc
```
I’ll decrypt the key using the password I set above so I don’t have to remember it:
```
openssl rsa -in file.key-enc -out file.key
```
And dump the certificate:
```
openssl pkcs12 -in file.pfx -clcerts -nokeys -out file.crt
```
Now it can be used for authentication, for example with `evil-winrm`
- `-c file.crt` - provide the public key certificate
- `-k file.key` - provide the private key
