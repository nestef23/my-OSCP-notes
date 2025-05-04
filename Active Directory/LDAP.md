Port(s) 
tcp/389 for unencrypted connections 
tcp/636 for encrypted connections using SSL/TLS

## Sniffing LDAP traffic
Setup simple nc listener and force target to send LDAP traffic
```
sudo nc -lvnp 389
```
