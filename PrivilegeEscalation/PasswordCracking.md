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
Hashcat needs to know explicitly what we want to crack, we use "mode" to specify it

https://hashcat.net/wiki/doku.php?id=example_hashes
```
hashcat -m 1710 -o results.txt hash.txt /usr/share/wordlists/rockyou.txt
# -m 1710 – mode
# -o results.txt – results
# hash.txt – hashes to be cracked
# /usr/share/wordlists/rockyou.txt – wordlist
```
## Hydra
