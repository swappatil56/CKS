Linux kernel namespaces:

Namespaces are for isolation

PID 
-> Isolates processes from each other
   one process cannot see others process
   Process ID 10 can exists multiple times, once in every namespace

Mount
-> Restrict access to mount or root filesystem

Network
-> Only access to certain network devices
   Firewall and Routing rules & socket port numbers
   Not able to see all traffics or contact all endpoint


User
-> Different set of User ids
   User(0) inside one ns can be different from user(0) inside other ns
   don't use the host-root user (0) inside container

###########################################################################################
Cgroups

Cgroups restrict the resource usage of process
e.g. RAM,CPU,Disk

###########################################################################################