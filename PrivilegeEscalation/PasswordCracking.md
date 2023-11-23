## Intro
This covers all scenarios where password may need to be cracked


## John
### Basic
Create txt file with found hashes / encrypted passwords and hope that John recognizes them.
```
# basic
john foundusers.txt

# use custom wordlist 
john --wordlist=/usr/share/wordlists/rockyou.txt foundusers.txt
```
## Hashcat

## Hydra
