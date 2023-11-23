## Intro
RPC is a weird thing

## Nmap
Use scripts to get more info about service
```
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount,rpcinfo <IP>
```
