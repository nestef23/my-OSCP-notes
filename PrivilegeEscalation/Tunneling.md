## Local tunneling
As stated, there are multiple options to take at this point when it comes to the actual port forwarding, but we will opt for local port forwarding (you can find the dynamic version in this document's appendix.) To use local port forwarding with SSH , you can use the ssh command with the -L option, followed by the local port, remote host and port, and the remote SSH server. For example, the following command will forward traffic from the local port 1234 to the remote server remote.example.com 's localhost interface on port 22 :
```
ssh -L <localport>:localhost:<remoteport> user@remote.example.com
ssh -L 1234:localhost:22 user@remote.example.com
ssh -L 1234:localhost:5432 christine@{target_IP}
```
