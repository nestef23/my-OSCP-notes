
## Intro
This service is generally useless before credentials are obtained

## SSH
Connecting to SSH
```
# Password
ssh -p <port> <user>@<IP>

# Certificate (located in the same directory)
nano id_rsa
chmod id_rsa 600
ssh -i id_rsa -p <port> <user>@<IP>
```
