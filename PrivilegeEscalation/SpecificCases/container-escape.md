## Docker
Verify that ir is in fact a container instance
```
cat /proc/1/cgroup
-> 11:memory:/docker/3a453ab39d3d[...]
```
Check mounted filesytems. There is a chance that host FS is mounted to docker container.
```
mount
df -h
```
Maybe we can change file permission, or add new files to the host?

Check open ports and services
```
# get the IP
ip a
ifconfig

# scan ports
for PORT in {0..1000}; do timeout 1 bash -c "</dev/tcp/<IP>/$PORT&>/dev/null" 2>/dev/null && echo "port $PORT is open"; done
```
Maybe there is an SSH open to log into thr host instance?
