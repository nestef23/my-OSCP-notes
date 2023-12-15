## AA


### Whisker
https://github.com/eladshamir/Whisker
Whisker is a C# tool for taking over Active Directory user and computer accounts by manipulating their `msDS-KeyCredentialLink` attribute, effectively adding "**Shadow Credentials**" to the target account.

To identify vulnerable users read `Find-InterestingDomainAcl` from AD Recon cheatsheet.

```
.\Whisker.exe add /target:<CN of vulnerable user>
```
