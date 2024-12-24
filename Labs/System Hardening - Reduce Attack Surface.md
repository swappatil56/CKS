Your team has decided to use kube-bench via a DaemonSet instead of installing via package manager.

Go ahead and remove the kube-bench package using the default package manager.

Solution->

apt show kube-bench

apt remove kube-bench


controlplane $ apt show kube-bench
Package: kube-bench
Version: 0.6.5
Status: install ok installed
Maintainer: Yoav Rotem <yoav.rotem@aquasec.com>
Installed-Size: 24.5 MB
Homepage: https://github.com/aquasecurity/kube-bench
Vendor: Aqua Security
Download-Size: unknown
APT-Manual-Installed: yes
APT-Sources: /var/lib/dpkg/status
Description: The Kubernetes Bench for Security is a Go application that checks whether Kubernetes is deployed according to security best practices

controlplane $ 

controlplane $ k get daemonsets --all-namespaces
NAMESPACE     NAME         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
kube-system   canal        1         1         1       1            1           kubernetes.io/os=linux   12d
kube-system   kube-proxy   1         1         1       1            1           kubernetes.io/os=linux   12d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apt-get remove kube-bench
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  kube-bench
0 upgraded, 0 newly installed, 1 to remove and 202 not upgraded.
After this operation, 24.5 MB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 132763 files and directories currently installed.)
Removing kube-bench (0.6.5) ...
dpkg: warning: while removing kube-bench, directory '/usr/local' not empty so not removed
controlplane $ 


#################################################

The package vsftpd has been installed.

Don't uninstall it, just stop the service.




controlplane $ service vsftpd status
● vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2024-12-19 04:55:22 UTC; 3min 44s ago
   Main PID: 22717 (vsftpd)
      Tasks: 1 (limit: 2338)
     Memory: 808.0K
     CGroup: /system.slice/vsftpd.service
             └─22717 /usr/sbin/vsftpd /etc/vsftpd.conf

Dec 19 04:55:22 controlplane systemd[1]: Starting vsftpd FTP server...
Dec 19 04:55:22 controlplane systemd[1]: Started vsftpd FTP server.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ service vsftpd stop  
controlplane $ service vsftpd status
● vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Thu 2024-12-19 04:59:14 UTC; 2s ago
    Process: 22717 ExecStart=/usr/sbin/vsftpd /etc/vsftpd.conf (code=killed, signal=TERM)
   Main PID: 22717 (code=killed, signal=TERM)

Dec 19 04:55:22 controlplane systemd[1]: Starting vsftpd FTP server...
Dec 19 04:55:22 controlplane systemd[1]: Started vsftpd FTP server.
Dec 19 04:59:14 controlplane systemd[1]: Stopping vsftpd FTP server...
Dec 19 04:59:14 controlplane systemd[1]: vsftpd.service: Succeeded.
Dec 19 04:59:14 controlplane systemd[1]: Stopped vsftpd FTP server.
controlplane $ 



############################################################################################################


There is an unwanted process running which listens on port 1234 .

Kill the process and delete the binary.



controlplane $ k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   12d   v1.31.0
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ netstat -plnt | grep 1234
tcp        0      0 0.0.0.0:1234            0.0.0.0:*               LISTEN      20904/app1          
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ lsof -i :1234
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
app1    20904 root    3u  IPv4 181037      0t0  TCP *:1234 (LISTEN)
controlplane $ 
controlplane $ 
controlplane $ kill -9 20904
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kill -9 20904
bash: kill: (20904) - No such process
controlplane $ lsof -i :1234
controlplane $ 
controlplane $ 
controlplane $ netstat -plnt | grep 1234
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ netstat -plnt | grep 1234
controlplane $ rm /usr/bin/app1
controlplane $ 


############################################################################################################
