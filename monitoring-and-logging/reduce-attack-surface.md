# disable service snapd via systemctl

controlplane $ systemctl status snapd
● snapd.service - Snap Daemon
     Loaded: loaded (/lib/systemd/system/snapd.service; disabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-12-18 10:05:59 UTC; 6min ago
TriggeredBy: ● snapd.socket
   Main PID: 814 (snapd)
      Tasks: 8 (limit: 2338)
     Memory: 31.5M
     CGroup: /system.slice/snapd.service
             └─814 /usr/lib/snapd/snapd

Dec 18 10:05:48 controlplane systemd[1]: Starting Snap Daemon...
Dec 18 10:05:49 controlplane snapd[814]: AppArmor status: apparmor is enabled and all features are available
Dec 18 10:05:58 controlplane snapd[814]: overlord.go:274: Acquiring state lock file
Dec 18 10:05:58 controlplane snapd[814]: overlord.go:279: Acquired state lock file
Dec 18 10:05:58 controlplane snapd[814]: daemon.go:250: started snapd/2.66.1 (series 16; classic) ubuntu/20.04 (amd64) linux/5.4.0-131-generic.
Dec 18 10:05:59 controlplane snapd[814]: daemon.go:353: adjusting startup timeout by 45s (pessimistic estimate of 30s plus 5s per snap)
Dec 18 10:05:59 controlplane snapd[814]: backends.go:58: AppArmor status: apparmor is enabled and all features are available (using snapd provided apparmor_parser)
Dec 18 10:05:59 controlplane systemd[1]: Started Snap Daemon.
Dec 18 10:06:00 controlplane snapd[814]: storehelpers.go:1044: cannot refresh: snap has no updates available: "core20", "lxd", "snapd"
controlplane $ 



controlplane $ systemctl stop snapd
Warning: Stopping snapd.service, but it can still be activated by:
  snapd.socket
controlplane $ 


controlplane $ systemctl disable snapd
controlplane $




controlplane $ systemctl list-units | grep snapd
  run-snapd-ns-lxd.mnt.mount                                                                                                                    loaded active mounted   /run/snapd/ns/lxd.mnt                                                                                                       
  run-snapd-ns.mount                                                                                                                            loaded active mounted   /run/snapd/ns                                                                                                               
  snap-snapd-23258.mount                                                                                                                        loaded active mounted   Mount unit for snapd, revision 23258                                                                                        
  snapd.apparmor.service                                                                                                                        loaded active exited    Load AppArmor profiles managed internally by snapd                                                                          
  snapd.seeded.service                                                                                                                          loaded active exited    Wait until snapd is fully seeded                                                                                            
  snapd.socket                                                                                                                                  loaded active listening Socket activation for snappy daemon                                                                                         
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ systemctl list-units --type=service --state=running | grep snapd
controlplane $ 


###########################################################################################


## install and investigate services

vsftpd
smbd(samba)


controlplane $ apt-get update
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://ppa.launchpad.net/rmescandon/yq/ubuntu focal InRelease
Hit:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease                                                         
Hit:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease                                                       
Hit:6 http://security.ubuntu.com/ubuntu focal-security InRelease                                 
Hit:5 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  InRelease
Reading package lists... Done
controlplane $ 


controlplane $ apt-get install vsftpd samba
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  attr ibverbs-providers libboost-iostreams1.71.0 libcephfs2 libibverbs1 librados2 librdmacm1 python3-crypto python3-dnspython python3-gpg python3-markdown python3-packaging
  python3-samba python3-tdb samba-common samba-common-bin samba-dsdb-modules samba-vfs-modules tdb-tools
Suggested packages:
  python-markdown-doc bind9 bind9utils ctdb ldb-tools ntp | chrony smbldap-tools winbind heimdal-clients
The following NEW packages will be installed:
  attr ibverbs-providers libboost-iostreams1.71.0 libcephfs2 libibverbs1 librados2 librdmacm1 python3-crypto python3-dnspython python3-gpg python3-markdown python3-packaging
  python3-samba python3-tdb samba samba-common samba-common-bin samba-dsdb-modules samba-vfs-modules tdb-tools vsftpd
0 upgraded, 21 newly installed, 0 to remove and 193 not upgraded.
Need to get 10.2 MB of archives.
After this operation, 68.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] y



controlplane $ systemctl status vsftpd
● vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-12-18 10:17:35 UTC; 56s ago
   Main PID: 10715 (vsftpd)
      Tasks: 1 (limit: 2338)
     Memory: 856.0K
     CGroup: /system.slice/vsftpd.service
             └─10715 /usr/sbin/vsftpd /etc/vsftpd.conf

Dec 18 10:17:35 controlplane systemd[1]: Starting vsftpd FTP server...
Dec 18 10:17:35 controlplane systemd[1]: Started vsftpd FTP server.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ systemctl status samba
Unit samba.service could not be found.
controlplane $ systemctl status smbd 
● smbd.service - Samba SMB Daemon
     Loaded: loaded (/lib/systemd/system/smbd.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-12-18 10:17:49 UTC; 1min 7s ago
       Docs: man:smbd(8)
             man:samba(7)
             man:smb.conf(5)
   Main PID: 11350 (smbd)
     Status: "smbd: ready to serve connections..."
      Tasks: 4 (limit: 2338)
     Memory: 17.8M
     CGroup: /system.slice/smbd.service
             ├─11350 /usr/sbin/smbd --foreground --no-process-group
             ├─11352 /usr/sbin/smbd --foreground --no-process-group
             ├─11353 /usr/sbin/smbd --foreground --no-process-group
             └─11354 /usr/lib/x86_64-linux-gnu/samba/samba-bgqd --ready-signal-fd=45 --parent-watch-fd=11 --debuglevel=0 -F

Dec 18 10:17:49 controlplane systemd[1]: Starting Samba SMB Daemon...
Dec 18 10:17:49 controlplane update-apparmor-samba-profile[11344]: grep: /etc/apparmor.d/samba/smbd-shares: No such file or directory
Dec 18 10:17:49 controlplane update-apparmor-samba-profile[11347]: diff: /etc/apparmor.d/samba/smbd-shares: No such file or directory
Dec 18 10:17:49 controlplane systemd[1]: Started Samba SMB Daemon.
controlplane $ 



controlplane $ ps -ef | grep vsftpd
root       10715       1  0 10:17 ?        00:00:00 /usr/sbin/vsftpd /etc/vsftpd.conf
root       12895    6209  0 10:19 pts/0    00:00:00 grep --color=auto vsftpd
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ps -ef | grep smbd  
root       11350       1  0 10:17 ?        00:00:00 /usr/sbin/smbd --foreground --no-process-group
root       11352   11350  0 10:17 ?        00:00:00 /usr/sbin/smbd --foreground --no-process-group
root       11353   11350  0 10:17 ?        00:00:00 /usr/sbin/smbd --foreground --no-process-group
root       13066    6209  0 10:20 pts/0    00:00:00 grep --color=auto smbd
controlplane $ 



controlplane $ netstat -plnt 
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.1:10257         0.0.0.0:*               LISTEN      1976/kube-controlle 
tcp        0      0 127.0.0.1:10259         0.0.0.0:*               LISTEN      2056/kube-scheduler 
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      1132/systemd-resolv 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      761/sshd: /usr/sbin 
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      568/cupsd           
tcp        0      0 0.0.0.0:445             0.0.0.0:*               LISTEN      11350/smbd          
tcp        0      0 0.0.0.0:40200           0.0.0.0:*               LISTEN      2076/kc-terminal    
tcp        0      0 127.0.0.1:10248         0.0.0.0:*               LISTEN      1602/kubelet        
tcp        0      0 127.0.0.1:10249         0.0.0.0:*               LISTEN      2752/kube-proxy     
tcp        0      0 127.0.0.1:36265         0.0.0.0:*               LISTEN      655/containerd      
tcp        0      0 0.0.0.0:139             0.0.0.0:*               LISTEN      11350/smbd          
tcp        0      0 127.0.0.1:9099          0.0.0.0:*               LISTEN      3793/calico-node    
tcp        0      0 172.30.1.2:2379         0.0.0.0:*               LISTEN      2009/etcd           
tcp        0      0 127.0.0.1:2379          0.0.0.0:*               LISTEN      2009/etcd           
tcp        0      0 172.30.1.2:2380         0.0.0.0:*               LISTEN      2009/etcd           
tcp        0      0 0.0.0.0:40205           0.0.0.0:*               LISTEN      1591/node           
tcp        0      0 127.0.0.1:2381          0.0.0.0:*               LISTEN      2009/etcd           
tcp6       0      0 :::40305                :::*                    LISTEN      1930/runtime-info-s 
tcp6       0      0 :::21                   :::*                    LISTEN      10715/vsftpd        
tcp6       0      0 :::22                   :::*                    LISTEN      761/sshd: /usr/sbin 
tcp6       0      0 ::1:631                 :::*                    LISTEN      568/cupsd           
tcp6       0      0 :::445                  :::*                    LISTEN      11350/smbd          
tcp6       0      0 :::10250                :::*                    LISTEN      1602/kubelet        
tcp6       0      0 :::6443                 :::*                    LISTEN      2020/kube-apiserver 
tcp6       0      0 :::139                  :::*                    LISTEN      11350/smbd          
tcp6       0      0 :::40300                :::*                    LISTEN      1527/runtime-scenar 
tcp6       0      0 :::10256                :::*                    LISTEN      2752/kube-proxy     
controlplane $ 

###########################################################################################


Find an application runnin on port 21 and disable it

controlplane $ 
controlplane $ netstat -plnt | grep 21
tcp6       0      0 :::21                   :::*                    LISTEN      10715/vsftpd        
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ lsof -i :21
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
vsftpd  10715 root    3u  IPv6 101501      0t0  TCP *:ftp (LISTEN)
controlplane $ 
controlplane $ 
controlplane $ 


controlplane $ systemctl status vsftpd
● vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-12-18 10:17:35 UTC; 8min ago
   Main PID: 10715 (vsftpd)
      Tasks: 1 (limit: 2338)
     Memory: 856.0K
     CGroup: /system.slice/vsftpd.service
             └─10715 /usr/sbin/vsftpd /etc/vsftpd.conf

Dec 18 10:17:35 controlplane systemd[1]: Starting vsftpd FTP server...
Dec 18 10:17:35 controlplane systemd[1]: Started vsftpd FTP server.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ systemctl stop vsftpd  
controlplane $ 
controlplane $ 
controlplane $ systemctl disable vsftpd
Synchronizing state of vsftpd.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable vsftpd
Removed /etc/systemd/system/multi-user.target.wants/vsftpd.service.
controlplane $ systemctl status vsftpd
● vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; disabled; vendor preset: enabled)
     Active: inactive (dead)

Dec 18 10:17:35 controlplane systemd[1]: Starting vsftpd FTP server...
Dec 18 10:17:35 controlplane systemd[1]: Started vsftpd FTP server.
Dec 18 10:26:35 controlplane systemd[1]: Stopping vsftpd FTP server...
Dec 18 10:26:35 controlplane systemd[1]: vsftpd.service: Succeeded.
Dec 18 10:26:35 controlplane systemd[1]: Stopped vsftpd FTP server.
controlplane $ 



controlplane $ netstat -plnt | grep 21
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ lsof -i :21
controlplane $ 


###########################################################################################################################


Investigate Linux users:

controlplane $ whoami
root
controlplane $ 
controlplane $ 
controlplane $ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
landscape:x:110:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:111:1::/var/cache/pollinate:/bin/false
fwupd-refresh:x:112:116:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
kc-internal:x:0:0::/root:/bin/bash
dnsmasq:x:113:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
rtkit:x:114:121:RealtimeKit,,,:/proc:/usr/sbin/nologin
lightdm:x:115:124:Light Display Manager:/var/lib/lightdm:/bin/false
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
avahi:x:117:126:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
cups-pk-helper:x:118:127:user for cups-pk-helper service,,,:/home/cups-pk-helper:/usr/sbin/nologin
pulse:x:119:128:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
geoclue:x:120:130::/var/lib/geoclue:/usr/sbin/nologin
saned:x:121:132::/var/lib/saned:/usr/sbin/nologin
colord:x:122:133:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
gdm:x:123:134:Gnome Display Manager:/var/lib/gdm3:/bin/false
nova:x:124:135::/var/lib/nova:/bin/bash
ftp:x:125:137:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
controlplane $ 




controlplane $ su ubuntu
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@controlplane:/root$ 
ubuntu@controlplane:/root$ 
ubuntu@controlplane:/root$ 
ubuntu@controlplane:/root$ whoami
ubuntu
ubuntu@controlplane:/root$ su -i
su: invalid option -- 'i'
Try 'su --help' for more information.
ubuntu@controlplane:/root$ su -
Password: 
su: Authentication failure
ubuntu@controlplane:/root$ sudo su -
controlplane $ 
controlplane $ 




controlplane $ ps aux | grep bash
root        1520  0.0  0.0   3896  1916 ?        S    10:05   0:00 bash -c export RV_SCRIPT_DIR=/var/run/kc-internal/scenario-service && mkdir -p $RV_SCRIPT_DIR;  /bin/runtime-scenario-service 
root        1580  0.0  0.0   3896  1896 ?        SN   10:05   0:00 bash -c set -x; cd /opt; while ! curl -o theia-install.sh https://storage.googleapis.com/killercoda-prod-europe1/theia/theia-install.sh?v=36074; do sleep 1; done; bash theia-install.sh; rm theia-install.sh; nice -n 19 /opt/theia/node /opt/theia/browser-app/src-gen/backend/main.js /root --hostname=0.0.0.0 --port 40205
root        2074  0.0  0.0   3896   152 ?        S    10:06   0:00 bash -c while true; do /bin/kc-terminal -p 40200 --writable -t disableLeaveAlert=true bash; done
root        2076  0.0  0.0  10832  1672 ?        Sl   10:06   0:00 /bin/kc-terminal -p 40200 --writable -t disableLeaveAlert true bash
root        6209  0.0  0.2   5440  4500 pts/0    Ss   10:11   0:00 bash
root        6314  0.0  0.2   5308  4360 pts/1    SNs+ 10:11   0:00 /bin/bash
ubuntu     17795  0.0  0.2   9996  4824 pts/0    S    10:29   0:00 bash
root       17970  0.1  0.2  10292  5236 pts/0    S    10:30   0:00 -bash
root       18224  0.0  0.1   8160  2524 pts/0    S+   10:30   0:00 grep --color=auto bash
controlplane $ 

###############################################

Investigate linux users


## adduser


controlplane $ adduser test
Adding user `test' ...
Adding new group `test' (1001) ...
Adding new user `test' (1001) with group `test' ...
Creating home directory `/home/test' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for test
Enter the new value, or press ENTER for the default
        Full Name []: test
        Room Number []: test
        Work Phone []: test
        Home Phone []: test
        Other []: test
Is the information correct? [Y/n] y
controlplane $ 
controlplane $ 
controlplane $ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
landscape:x:110:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:111:1::/var/cache/pollinate:/bin/false
fwupd-refresh:x:112:116:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
kc-internal:x:0:0::/root:/bin/bash
dnsmasq:x:113:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
rtkit:x:114:121:RealtimeKit,,,:/proc:/usr/sbin/nologin
lightdm:x:115:124:Light Display Manager:/var/lib/lightdm:/bin/false
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
avahi:x:117:126:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
cups-pk-helper:x:118:127:user for cups-pk-helper service,,,:/home/cups-pk-helper:/usr/sbin/nologin
pulse:x:119:128:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
geoclue:x:120:130::/var/lib/geoclue:/usr/sbin/nologin
saned:x:121:132::/var/lib/saned:/usr/sbin/nologin
colord:x:122:133:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
gdm:x:123:134:Gnome Display Manager:/var/lib/gdm3:/bin/false
nova:x:124:135::/var/lib/nova:/bin/bash
ftp:x:125:137:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
test:x:1001:1001:test,test,test,test,test:/home/test:/bin/bash
controlplane $ 



controlplane $ su test
test@controlplane:/root$ 
test@controlplane:/root$ 
test@controlplane:/root$ 
test@controlplane:/root$ whoami
test
test@controlplane:/root$ 
test@controlplane:/root$ sudo su -i
[sudo] password for test: 
test is not in the sudoers file.  This incident will be reported.
test@controlplane:/root$ 
test@controlplane:/root$ 
test@controlplane:/root$ 
test@controlplane:/root$ 
test@controlplane:/root$ exit
exit
controlplane $ 

