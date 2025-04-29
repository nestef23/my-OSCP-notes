
## Intro
This service is generally useless before credentials are obtained

## SSH
Connecting to SSH
```
# Password
ssh -p <port> <user>@<IP>

# Certificate (located in the same directory)
nano id_rsa
chmod id_rsa 400
ssh -i id_rsa -p <port> <user>@<IP>
```
## SSH keys
We can decrypt RSA key if we have encrypted key and password
```
# If the key is in the hex code
cat id_rsa | xxd -r -p > id_rsa_encrypted

# It should look like this now
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,AEB88C140F69BF2074788DE24AE48D46

DbPrO78kegNuk1DAqlAN5jbjXv0PPsog3jdbMFS8iE9p3UOL0lF0xf7PzmrkDa8R
5y/b46+9nEpCMfTPhNuJRcW2U2gJcOFH+9RJDBC5UJMUS1/gjB/7/My00Mwx+aI6
0EI0SbOYUAV1W4EV7m96QsZjrwJvnjVafm6VsKaTPBHpugcASvMqz76W6abRZeXi
[...]
l0ln9L1b/NXpHjGa8WHHTjoIilB5qNUyywSeTBF2awRlXH9BrkZG4Fc4gdmW/IzT
RUgZkbMQZNIIfzj1QuilRVBm/F76Y/YMrmnM9k/1xSGIskwCUQ+95CGHJE8MkhD3
-----END RSA PRIVATE KEY-----

# Decode the key and supply password
openssl rsa -in id_rsa_encrypted -out id_rsa_decrypted
```
