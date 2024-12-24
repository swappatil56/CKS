
Question 9 | AppArmor Profile
Task weight: 3%
Use context: kubectl config use-context workload-prod

Some containers need to run more secure and restricted. There is an existing AppArmor profile located at /opt/course/9/profile for this.

Install the AppArmor profile on Node cluster1-node1. Connect using ssh cluster1-node1.

Add label security=apparmor to the Node

Create a Deployment named apparmor in Namespace default with:

One replica of image nginx:1.19.2
NodeSelector for security=apparmor
Single container named c1 with the AppArmor profile enabled
The Pod might not run properly with the profile enabled. Write the logs of the Pod into /opt/course/9/logs so another team can work on getting the application running.










node01 $ vi profile
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor_status   
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
   /usr/sbin/dhclient (667) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (794) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (1013) /{,usr/}sbin/dhclient
   /coredns (2350) cri-containerd.apparmor.d
   /coredns (2359) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor_parser profile
node01 $ apparmor_status
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
   /usr/sbin/dhclient (667) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (794) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (1013) /{,usr/}sbin/dhclient
   /coredns (2350) cri-containerd.apparmor.d
   /coredns (2359) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ 
node01 $ 




controlplane $ cat deploy.yaml 




apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: apparmor
  name: apparmor
spec:
  replicas: 1
  selector:
    matchLabels:
      app: apparmor
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: apparmor
    spec:
      nodeSelector: 
             security: apparmor
      containers:
      - image: nginx:1.19.2
        name: c1
        resources: {}
        securityContext:
          appArmorProfile:
               type: Localhost
               localhostProfile: docker-nginx
status: {}
controlplane $ 






################################################################################################################
You're asked to verify if the following AppArmor profiles are available on node01 :

docker-default
snap.lxd.lxc
ftpd
/usr/sbin/tcpdump
Create file /root/profiles.txt on node controlplane . It should contain only these profile names that are available on node01 .





node01 $ apparmor_status
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
   /usr/sbin/dhclient (717) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (817) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (846) /{,usr/}sbin/dhclient
   /coredns (3286) cri-containerd.apparmor.d
   /coredns (3453) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor status| grep docker-default
apparmor: command not found
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor_status| grep docker-default
   docker-default
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor_status | grep snap.lxd.lxc 
   snap.lxd.lxc
   snap.lxd.lxc-to-lxd
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor_status | grep ftpd
node01 $ 
node01 $ 
node01 $ apparmor_status | grep /usr/sbin/tcpdump
   /usr/sbin/tcpdump
node01 $ 

####################################################################################################################################

There is an existing Deployment named spacecow in Namespace moon .

It should be configured to use AppArmor profile docker-default , but something seems wrong.

Fix it.



controlplane $ k get deploy -n moon
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
spacecow   0/3     3            0           7m24s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n moon
NAME                        READY   STATUS                 RESTARTS   AGE
spacecow-64fdff66c6-26qcz   0/1     CreateContainerError   0          7m31s
spacecow-64fdff66c6-bcb9q   0/1     CreateContainerError   0          7m31s
spacecow-64fdff66c6-sr4lc   0/1     CreateContainerError   0          7m31s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k describe pod spacecow-64fdff66c6-26qcz -n moons
Error from server (NotFound): namespaces "moons" not found
controlplane $ k describe pod spacecow-64fdff66c6-26qcz -n moon  
Name:             spacecow-64fdff66c6-26qcz
Namespace:        moon
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Thu, 19 Dec 2024 05:02:36 +0000
Labels:           app=spacecow
                  pod-template-hash=64fdff66c6
Annotations:      cni.projectcalico.org/containerID: 9130b68b8a6692d90a96e2c3617583fba51c9e9171f75fbe25dc626d65373d77
                  cni.projectcalico.org/podIP: 192.168.1.6/32
                  cni.projectcalico.org/podIPs: 192.168.1.6/32
                  container.apparmor.security.beta.kubernetes.io/httpd: localhost/docker
Status:           Pending
IP:               192.168.1.6
IPs:
  IP:           192.168.1.6
Controlled By:  ReplicaSet/spacecow-64fdff66c6
Containers:
  httpd:
    Container ID:   
    Image:          httpd:2.4.52-alpine
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       CreateContainerError
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8zm8b (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-8zm8b:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                     From               Message
  ----     ------     ----                    ----               -------
  Normal   Scheduled  7m43s                   default-scheduler  Successfully assigned moon/spacecow-64fdff66c6-26qcz to node01
  Normal   Pulling    7m43s                   kubelet            Pulling image "httpd:2.4.52-alpine"
  Normal   Pulled     7m37s                   kubelet            Successfully pulled image "httpd:2.4.52-alpine" in 405ms (5.555s including waiting). Image size: 18209719 bytes.
  Warning  Failed     5m26s (x12 over 7m37s)  kubelet            Error: failed to get container spec opts: failed to generate apparmor spec opts: apparmor profile not found docker
  Normal   Pulled     2m35s (x24 over 7m37s)  kubelet            Container image "httpd:2.4.52-alpine" already present on machine
controlplane $ 



####################################################################################################################################


There is an AppArmor profile at /root/profile .

It should be referenced by name docker-nginx-custom , change the profile if needed.

Install it on nodes controlplane and node01 .



controlplane $ cat /root/profile
#include <tunables/global>

profile docker-nginx flags=(attach_disconnected,mediate_deleted) {
  #include <abstractions/base>

  network inet tcp,
  network inet udp,
  network inet icmp,

  deny network raw,

  deny network packet,

  file,
  umount,

  deny /bin/** wl,
  deny /boot/** wl,
  deny /dev/** wl,
  deny /etc/** wl,
  deny /home/** wl,
  deny /lib/** wl,
  deny /lib64/** wl,
  deny /media/** wl,
  deny /mnt/** wl,
  deny /opt/** wl,
  deny /proc/** wl,
  deny /root/** wl,
  deny /sbin/** wl,
  deny /srv/** wl,
  deny /tmp/** wl,
  deny /sys/** wl,
  deny /usr/** wl,

  audit /** w,

  /var/run/nginx.pid w,

  /usr/sbin/nginx ix,

  deny /bin/dash mrwklx,
  deny /bin/sh mrwklx,
  deny /usr/bin/top mrwklx,


  capability chown,
  capability dac_override,
  capability setuid,
  capability setgid,
  capability net_bind_service,

  deny @{PROC}/* w,   # deny write for all files directly in /proc (not in a subdir)
  # deny write to files not in /proc/<number>/** or /proc/sys/**
  deny @{PROC}/{[^1-9],[^1-9][^0-9],[^1-9s][^0-9y][^0-9s],[^1-9][^0-9][^0-9][^0-9]*}/** w,
  deny @{PROC}/sys/[^k]** w,  # deny /proc/sys except /proc/sys/k* (effectively /proc/sys/kernel)
  deny @{PROC}/sys/kernel/{?,??,[^s][^h][^m]**} w,  # deny everything except shm* in /proc/sys/kernel/
  deny @{PROC}/sysrq-trigger rwklx,
  deny @{PROC}/mem rwklx,
  deny @{PROC}/kmem rwklx,
  deny @{PROC}/kcore rwklx,

  deny mount,

  deny /sys/[^f]*/** wklx,
  deny /sys/f[^s]*/** wklx,
  deny /sys/fs/[^c]*/** wklx,
  deny /sys/fs/c[^g]*/** wklx,
  deny /sys/fs/cg[^r]*/** wklx,
  deny /sys/firmware/** rwklx,
  deny /sys/kernel/security/** rwklx,
}controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /root/profile
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apparmor_parser /root/profile
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apparmor_status 
apparmor module is loaded.
38 profiles are loaded.
38 profiles are in enforce mode.
   /snap/snapd/23258/usr/lib/snapd/snap-confine
   /snap/snapd/23258/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/bin/man
   /usr/lib/NetworkManager/nm-dhcp-client.action
   /usr/lib/NetworkManager/nm-dhcp-helper
   /usr/lib/connman/scripts/dhclient-script
   /usr/lib/cups/backend/cups-pdf
   /usr/lib/lightdm/lightdm-guest-session
   /usr/lib/lightdm/lightdm-guest-session//chromium
   /usr/lib/snapd/snap-confine
   /usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/sbin/cups-browsed
   /usr/sbin/cupsd
   /usr/sbin/cupsd//third_party
   /usr/sbin/tcpdump
   /{,usr/}sbin/dhclient
   cri-containerd.apparmor.d
   docker-default
   docker-nginx-custom
   ippusbxd
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
11 processes have profiles defined.
11 processes are in enforce mode.
   /usr/sbin/cups-browsed (653) 
   /usr/sbin/cupsd (571) 
   /usr/sbin/dhclient (766) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (895) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (947) /{,usr/}sbin/dhclient
   /usr/local/bin/kube-apiserver (1828) cri-containerd.apparmor.d
   /usr/local/bin/kube-controller-manager (1898) cri-containerd.apparmor.d
   /usr/local/bin/kube-scheduler (1906) cri-containerd.apparmor.d
   /usr/local/bin/etcd (1907) cri-containerd.apparmor.d
   /usr/bin/kube-controllers (3795) cri-containerd.apparmor.d
   /usr/bin/local-path-provisioner (4076) cri-containerd.apparmor.d
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ scp /root/profile root@node01
controlplane $ 
controlplane $ scp /root/profile root@node01:/root
profile                                                                                                                                                  100% 1650     3.2MB/s   00:00    
controlplane $ 
controlplane $ 



node01 $ vi /root/profile
node01 $ apparmor_parser /root/profile
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ apparmor_status
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
   docker-nginx-custom
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
17 processes have profiles defined.
17 processes are in enforce mode.
   /usr/sbin/dhclient (717) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (817) /{,usr/}sbin/dhclient
   /usr/sbin/dhclient (846) /{,usr/}sbin/dhclient
   /coredns (3286) cri-containerd.apparmor.d
   /coredns (3453) cri-containerd.apparmor.d
   /usr/local/apache2/bin/httpd (6733) docker-default
   /usr/local/apache2/bin/httpd (6744) docker-default
   /usr/local/apache2/bin/httpd (6745) docker-default
   /usr/local/apache2/bin/httpd (6746) docker-default
   /usr/local/apache2/bin/httpd (6995) docker-default
   /usr/local/apache2/bin/httpd (7007) docker-default
   /usr/local/apache2/bin/httpd (7008) docker-default
   /usr/local/apache2/bin/httpd (7009) docker-default
   /usr/local/apache2/bin/httpd (7286) docker-default
   /usr/local/apache2/bin/httpd (7297) docker-default
   /usr/local/apache2/bin/httpd (7298) docker-default
   /usr/local/apache2/bin/httpd (7299) docker-default
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
node01 $ 



#################################################################################################################


