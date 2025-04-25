## Registry hives
The SAM ( Security Account Manager ) file on Windows is used as a database to store the hashes for the users on Windows. 
We can extract hashes from it and attempt to crack them.
To crack the DB we need the SAM and SYSTEM hives. 
They are located at `C:\WIndows\System32\config\SAM` and `C:\Windows\System32\config\SYSTEM`. 

## Cracking SAM & SYSTEM
We can obtain the hashes using samdump2
```
# Supply two hives in THIS order
samdump2 SYSTEM SAM
```
Once we have the hashes, we can crack them with john or hashcat.
