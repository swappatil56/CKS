## setup simple apparmor profile for curl


node01 $ aa-

Command 'aa-' not found, did you mean:

  command 'aa' from deb astronomical-almanac (5.6-6)

Try: apt install <deb name>

node01 $ 
node01 $ 
node01 $ 
node01 $ aa-status
apparmor module is loaded.
32 profiles are loaded.
32 profiles are in enforce mode.
   /snap/snapd/17336/usr/lib/snapd/snap-confine
   /snap/snapd/17336/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /snap/snapd/23258/usr/lib/snapd/snap-confine
   /snap/snapd/23258/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/bin/man
   /usr/lib/NetworkManager/nm-dhcp-client.action
   /usr/lib/NetworkManager/nm-dhcp-helper
   /usr/lib/connman/scripts/dhclient-script
   /usr/lib/snapd/snap-confine
   /usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/sbin/tcpdump
   /{,usr/}sbin/dhclient
   cri-containerd.apparmor.d
   docker-default
   lsb_release
   man_filter
   man_groff
   nvidia_modprobe
   nvidia_modprobe//kmod
   snap-update-ns.lxd
   snap.lxd.activate
   snap.lxd.benchmark
   snap.lxd.buginfo
   snap.lxd.check-kernel
   snap.lxd.daemon
   snap.lxd.hook.configure
   snap.lxd.hook.install
   snap.lxd.hook.remove
   snap.lxd.lxc
   snap.lxd.lxc-to-lxd
   snap.lxd.lxd
   snap.lxd.migrate
0 profiles are in complain mode.
5 processes have profiles defined.
5 processes are in enforce mode.
   /usr/sbin/dhclient (637) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (742) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (801) /{,usr/}sbin/dhclient
   /coredns (3379) cri-containerd.apparmor.d
   /coredns (3543) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ 
node01 $ 
node01 $ 
node01 $ apt-get install apparmor-utils
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  python3-apparmor python3-libapparmor
Suggested packages:
  vim-addon-manager
The following NEW packages will be installed:
  apparmor-utils python3-apparmor python3-libapparmor
0 upgraded, 3 newly installed, 0 to remove and 194 not upgraded.
Need to get 158 kB of archives.
After this operation, 989 kB of additional disk space will be used.

Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-libapparmor amd64 2.13.3-7ubuntu5.4 [26.9 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-apparmor amd64 2.13.3-7ubuntu5.4 [79.8 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 apparmor-utils amd64 2.13.3-7ubuntu5.4 [51.1 kB]
Fetched 158 kB in 2s (104 kB/s)      
Selecting previously unselected package python3-libapparmor.
(Reading database ... 73016 files and directories currently installed.)
Preparing to unpack .../python3-libapparmor_2.13.3-7ubuntu5.4_amd64.deb ...
Unpacking python3-libapparmor (2.13.3-7ubuntu5.4) ...
Selecting previously unselected package python3-apparmor.
Preparing to unpack .../python3-apparmor_2.13.3-7ubuntu5.4_amd64.deb ...
Unpacking python3-apparmor (2.13.3-7ubuntu5.4) ...
Selecting previously unselected package apparmor-utils.
Preparing to unpack .../apparmor-utils_2.13.3-7ubuntu5.4_amd64.deb ...
Unpacking apparmor-utils (2.13.3-7ubuntu5.4) ...
Setting up python3-libapparmor (2.13.3-7ubuntu5.4) ...
Setting up python3-apparmor (2.13.3-7ubuntu5.4) ...
Setting up apparmor-utils (2.13.3-7ubuntu5.4) ...
Processing triggers for man-db (2.9.1-1) ...
node01 $ 



ode01 $ aa-status
apparmor module is loaded.
32 profiles are loaded.
32 profiles are in enforce mode.
   /snap/snapd/17336/usr/lib/snapd/snap-confine
   /snap/snapd/17336/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /snap/snapd/23258/usr/lib/snapd/snap-confine
   /snap/snapd/23258/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/bin/man
   /usr/lib/NetworkManager/nm-dhcp-client.action
   /usr/lib/NetworkManager/nm-dhcp-helper
   /usr/lib/connman/scripts/dhclient-script
   /usr/lib/snapd/snap-confine
   /usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/sbin/tcpdump
   /{,usr/}sbin/dhclient
   cri-containerd.apparmor.d
   docker-default
   lsb_release
   man_filter
   man_groff
   nvidia_modprobe
   nvidia_modprobe//kmod
   snap-update-ns.lxd
   snap.lxd.activate
   snap.lxd.benchmark
   snap.lxd.buginfo
   snap.lxd.check-kernel
   snap.lxd.daemon
   snap.lxd.hook.configure
   snap.lxd.hook.install
   snap.lxd.hook.remove
   snap.lxd.lxc
   snap.lxd.lxc-to-lxd
   snap.lxd.lxd
   snap.lxd.migrate
0 profiles are in complain mode.
5 processes have profiles defined.
5 processes are in enforce mode.
   /usr/sbin/dhclient (637) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (742) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (801) /{,usr/}sbin/dhclient
   /coredns (3379) cri-containerd.apparmor.d
   /coredns (3543) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ aa-genprof curl
Writing updated profile for /usr/bin/curl.
Setting /usr/bin/curl to complain mode.

Before you begin, you may wish to check if a
profile already exists for the application you
wish to confine. See the following wiki page for
more information:
https://gitlab.com/apparmor/apparmor/wikis/Profiles

Profiling: /usr/bin/curl

Please start the application to be profiled in
another window and exercise its functionality now.

Once completed, select the "Scan" option below in 
order to scan the system logs for AppArmor events. 

For each AppArmor event, you will be given the 
opportunity to choose whether the access should be 
allowed or denied.

[(S)can system log for AppArmor events] / (F)inish
Reading log entries from /var/log/syslog.
Updating AppArmor profiles in /etc/apparmor.d.
Segmentation fault (core dumped)
node01 $ aa-genprof curl

Before you begin, you may wish to check if a
profile already exists for the application you
wish to confine. See the following wiki page for
more information:
https://gitlab.com/apparmor/apparmor/wikis/Profiles

Profiling: /usr/bin/curl

Please start the application to be profiled in
another window and exercise its functionality now.

Once completed, select the "Scan" option below in 
order to scan the system logs for AppArmor events. 

For each AppArmor event, you will be given the 
opportunity to choose whether the access should be 
allowed or denied.

[(S)can system log for AppArmor events] / (F)inish

Reloaded AppArmor profiles in enforce mode.

Please consider contributing your new profile!
See the following wiki page for more information:
https://gitlab.com/apparmor/apparmor/wikis/Profiles

Finished generating profile for /usr/bin/curl.
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ curl killer.sh -v
*   Trying 104.26.10.136:80...
* TCP_NODELAY set
* Connected to killer.sh (104.26.10.136) port 80 (#0)
> GET / HTTP/1.1
> Host: killer.sh
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 301 Moved Permanently
< Date: Wed, 18 Dec 2024 07:10:59 GMT
< Content-Type: text/html
< Content-Length: 167
< Connection: keep-alive
< Cache-Control: max-age=3600
< Expires: Wed, 18 Dec 2024 08:10:59 GMT
< Location: https://killer.sh/
< Report-To: {"endpoints":[{"url":"https:\/\/a.nel.cloudflare.com\/report\/v4?s=LqOulqI7gv39cjBTgVMUdC09TiSmLzkDVeDxeKVReX185%2FcxU9QhLwek1L5YdBeWv04HXLQPZssey3u67cC1dHp9mp0Gg6uByKC1BrTfVnbsum6PEyqbhJF3cA%3D%3D"}],"group":"cf-nel","max_age":604800}
< NEL: {"success_fraction":0,"report_to":"cf-nel","max_age":604800}
< X-Content-Type-Options: nosniff
< Server: cloudflare
< CF-RAY: 8f3d56181e892e53-BOM
< server-timing: cfL4;desc="?proto=TCP&rtt=2649&min_rtt=2649&rtt_var=1324&sent=1&recv=3&lost=0&retrans=0&sent_bytes=0&recv_bytes=73&delivery_rate=0&cwnd=248&unsent_bytes=0&cid=0000000000000000&ts=0&x=0"
< 
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>cloudflare</center>
</body>
</html>
* Connection #0 to host killer.sh left intact
node01 $ 
node01 $ 
node01 $ 
node01 $ aa-profile
aa-profile: command not found
node01 $ aa-profiles
aa-profiles: command not found
node01 $ 
node01 $ 
node01 $ 
node01 $ aa-status
apparmor module is loaded.
33 profiles are loaded.
32 profiles are in enforce mode.
   /snap/snapd/17336/usr/lib/snapd/snap-confine
   /snap/snapd/17336/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /snap/snapd/23258/usr/lib/snapd/snap-confine
   /snap/snapd/23258/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/bin/man
   /usr/lib/NetworkManager/nm-dhcp-client.action
   /usr/lib/NetworkManager/nm-dhcp-helper
   /usr/lib/connman/scripts/dhclient-script
   /usr/lib/snapd/snap-confine
   /usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/sbin/tcpdump
   /{,usr/}sbin/dhclient
   cri-containerd.apparmor.d
   docker-default
   lsb_release
   man_filter
   man_groff
   nvidia_modprobe
   nvidia_modprobe//kmod
   snap-update-ns.lxd
   snap.lxd.activate
   snap.lxd.benchmark
   snap.lxd.buginfo
   snap.lxd.check-kernel
   snap.lxd.daemon
   snap.lxd.hook.configure
   snap.lxd.hook.install
   snap.lxd.hook.remove
   snap.lxd.lxc
   snap.lxd.lxc-to-lxd
   snap.lxd.lxd
   snap.lxd.migrate
1 profiles are in complain mode.
   /usr/bin/curl
5 processes have profiles defined.
5 processes are in enforce mode.
   /usr/sbin/dhclient (637) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (742) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (801) /{,usr/}sbin/dhclient
   /coredns (3379) cri-containerd.apparmor.d
   /coredns (3543) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ cd /etc/app
apparmor/   apparmor.d/ apport/     
node01 $ cd /etc/apparmor.d/
node01 $ ls
abstractions  force-complain  lsb_release      sbin.dhclient  usr.bin.curl  usr.lib.snapd.snap-confine.real  usr.sbin.tcpdump
disable       local           nvidia_modprobe  tunables       usr.bin.man   usr.sbin.rsyslogd
node01 $ vi usr.bin.curl
node01 $ 
node01 $ 
node01 $ aa-logprof
Reading log entries from /var/log/syslog.
Updating AppArmor profiles in /etc/apparmor.d.
Segmentation fault (core dumped)
node01 $ curl killer.sh -v
*   Trying 172.67.68.150:80...
* TCP_NODELAY set
* Connected to killer.sh (172.67.68.150) port 80 (#0)
> GET / HTTP/1.1
> Host: killer.sh
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 301 Moved Permanently
< Date: Wed, 18 Dec 2024 07:15:30 GMT
< Content-Type: text/html
< Content-Length: 167
< Connection: keep-alive
< Cache-Control: max-age=3600
< Expires: Wed, 18 Dec 2024 08:15:30 GMT
< Location: https://killer.sh/
< Report-To: {"endpoints":[{"url":"https:\/\/a.nel.cloudflare.com\/report\/v4?s=obEgwFNadN9J5zvGLPZwyKuIYdLu7Qrsk%2BjMQldzpVLCwZXK8aPSTv48NsmxsBe59HRHWcI20zDioXGjZMfqie16AAElHl0k8HU8WFkC6%2FFg%2BAl3WT%2Fa17dkvw%3D%3D"}],"group":"cf-nel","max_age":604800}
< NEL: {"success_fraction":0,"report_to":"cf-nel","max_age":604800}
< X-Content-Type-Options: nosniff
< Server: cloudflare
< CF-RAY: 8f3d5cb15b6146a8-BOM
< server-timing: cfL4;desc="?proto=TCP&rtt=3023&min_rtt=3023&rtt_var=1511&sent=1&recv=3&lost=0&retrans=0&sent_bytes=0&recv_bytes=73&delivery_rate=0&cwnd=245&unsent_bytes=0&cid=0000000000000000&ts=0&x=0"
< 
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>cloudflare</center>
</body>
</html>
* Connection #0 to host killer.sh left intact
node01 $ 
node01 $ 


#####################################################################


## Nginx docker containers uses apparmor profile



node01 $ vi /etc/app
apparmor/   apparmor.d/ apport/     
node01 $ vi /etc/app
apparmor/   apparmor.d/ apport/     
node01 $ vi /etc/apparmor.d/docker-nginx
node01 $ 
node01 $ 




node01 $ 
node01 $ apparmor_parser /etc/apparmor.d/docker-nginx    
node01 $







node01 $ aa-status
apparmor module is loaded.
33 profiles are loaded.
33 profiles are in enforce mode.
   /snap/snapd/17336/usr/lib/snapd/snap-confine
   /snap/snapd/17336/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /snap/snapd/23258/usr/lib/snapd/snap-confine
   /snap/snapd/23258/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/bin/man
   /usr/lib/NetworkManager/nm-dhcp-client.action
   /usr/lib/NetworkManager/nm-dhcp-helper
   /usr/lib/connman/scripts/dhclient-script
   /usr/lib/snapd/snap-confine
   /usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/sbin/tcpdump
   /{,usr/}sbin/dhclient
   cri-containerd.apparmor.d
   docker-default
   docker-nginx
   lsb_release
   man_filter
   man_groff
   nvidia_modprobe
   nvidia_modprobe//kmod
   snap-update-ns.lxd
   snap.lxd.activate
   snap.lxd.benchmark
   snap.lxd.buginfo
   snap.lxd.check-kernel
   snap.lxd.daemon
   snap.lxd.hook.configure
   snap.lxd.hook.install
   snap.lxd.hook.remove
   snap.lxd.lxc
   snap.lxd.lxc-to-lxd
   snap.lxd.lxd
   snap.lxd.migrate
0 profiles are in complain mode.
5 processes have profiles defined.
5 processes are in enforce mode.
   /usr/sbin/dhclient (685) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (770) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (806) /{,usr/}sbin/dhclient
   /coredns (3612) cri-containerd.apparmor.d
   /coredns (3793) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ 




node01 $ docker run nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete 
650ee30bbe5e: Pull complete 
8cc1569e58f5: Pull complete 
362f35df001b: Pull complete 
13e320bf29cd: Pull complete 
7b50399908e1: Pull complete 
57b64962dd94: Pull complete 
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/18 07:27:09 [notice] 1#1: using the "epoll" event method
2024/12/18 07:27:09 [notice] 1#1: nginx/1.27.3
2024/12/18 07:27:09 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/18 07:27:09 [notice] 1#1: OS: Linux 5.4.0-131-generic
2024/12/18 07:27:09 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/18 07:27:09 [notice] 1#1: start worker processes
2024/12/18 07:27:09 [notice] 1#1: start worker process 28



node01 $ docker run --security-opt apparmor=docker-default nginx
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/18 07:29:32 [notice] 1#1: using the "epoll" event method
2024/12/18 07:29:32 [notice] 1#1: nginx/1.27.3
2024/12/18 07:29:32 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/18 07:29:32 [notice] 1#1: OS: Linux 5.4.0-131-generic
2024/12/18 07:29:32 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/18 07:29:32 [notice] 1#1: start worker processes
2024/12/18 07:29:32 [notice] 1#1: start worker process 28 .





node01 $ docker run --security-opt apparmor=docker-nginx nginx
/docker-entrypoint.sh: No files found in /docker-entrypoint.d/, skipping configuration
/docker-entrypoint.sh: 13: cannot create /dev/null: Permission denied
2024/12/18 07:30:11 [notice] 1#1: using the "epoll" event method
2024/12/18 07:30:11 [notice] 1#1: nginx/1.27.3
2024/12/18 07:30:11 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/18 07:30:11 [notice] 1#1: OS: Linux 5.4.0-131-generic
2024/12/18 07:30:11 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/18 07:30:11 [notice] 1#1: start worker processes
2024/12/18 07:30:11 [notice] 1#1: start worker process 8



node01 $ docker run --security-opt apparmor=docker-nginx -d nginx
6de7dfb14dae458358cef3018c0627c0795f239caf73bd2dfe3b7e322a1ec837
node01 $ 
node01 $ 
node01 $ 
node01 $ docker exec -it 6de7dfb14dae458358cef3018c0627c0795f239caf73bd2dfe3b7e322a1ec837 sh
# 
# 
# 
# touch /root/test
touch: cannot touch '/root/test': Permission denied
# 
# 
# sh
# 