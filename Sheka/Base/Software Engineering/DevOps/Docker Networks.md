22.12.2020  13:51
Tags: #dev | #job
____

# Docker Networks
## Console's commands for networks
 
```
docker network ls
docker network inspect name
```


## Single Host Networking

### Bridge

Bridge networks are usually used when your applications run in standalone containers that need to communicate. It works only on Linux.
![[Pasted image 20201222143426.png]]

### Host

Allows to share ports between containers and host OS. Only one container can use the same host port 
![[Pasted image 20201226132951.png]]

### Overlay

Applied for Docker EE/Swarm, allows to connect multiple Docker hosts
![[Pasted image 20201226133016.png]]

### Macvlan

Clone host interfaces and create virtual interfaces
![[Pasted image 20201226133036.png]]

____ 
###  Links 
- [[Docker]]
