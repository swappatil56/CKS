
Use kube-bench to ensure 1.2.20 has status PASS.


Solution

Check for results

# see all
kube-bench run --targets master

# or just see the one
kube-bench run --targets master --check 1.2.20

Fix the /etc/kubernetes/manifests/kube-apiserver.yaml


...
containers:
  - command:
    - kube-apiserver
    - --profiling=false
...
    image: registry.k8s.io/kube-apiserver:v1.22.2
...
Now wait for container to be restarted: watch crictl ps

############################################################################

Use kube-bench to ensure 1.3.2 has status PASS.


Solution

Check for results

# see all
kube-bench run --targets master

# or just see the one
kube-bench run --targets master --check 1.3.2

Fix the /etc/kubernetes/manifests/kube-controller-manager.yaml


...
  containers:
  - command:
    - kube-controller-manager
    - --profiling=false
...
    image: registry.k8s.io/kube-controller-manager:v1.22.2
...


############################################################################


Use kube-bench to ensure 1.1.19 has status PASS.

controlplane $ kube-bench run --targets master --check 1.1.19
[INFO] 1 Master Node Security Configuration
[INFO] 1.1 Master Node Configuration Files
[FAIL] 1.1.19 Ensure that the Kubernetes PKI directory and file ownership is set to root:root (Automated)

== Remediations master ==
1.1.19 Run the below command (based on the file location on your system) on the master node.
For example,
chown -R root:root /etc/kubernetes/pki/


== Summary master ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

== Summary total ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

controlplane $ 
controlplane $ ll /etc/kubernetes/pki/
total 68
drwxr-xr-x 3 root ubuntu 4096 Dec  6 09:13 ./
drwxrwxr-x 4 root root   4096 Dec  6 09:13 ../
-rw-r--r-- 1 root root   1123 Dec  6 09:13 apiserver-etcd-client.crt
-rw------- 1 root root   1679 Dec  6 09:13 apiserver-etcd-client.key
-rw-r--r-- 1 root root   1176 Dec  6 09:13 apiserver-kubelet-client.crt
-rw------- 1 root root   1675 Dec  6 09:13 apiserver-kubelet-client.key
-rw-r--r-- 1 root root   1289 Dec  6 09:13 apiserver.crt
-rw------- 1 root root   1679 Dec  6 09:13 apiserver.key
-rw-r--r-- 1 root root   1107 Dec  6 09:13 ca.crt
-rw------- 1 root root   1679 Dec  6 09:13 ca.key
drwxr-xr-x 2 root root   4096 Dec  6 09:13 etcd/
-rw-r--r-- 1 root root   1123 Dec  6 09:13 front-proxy-ca.crt
-rw------- 1 root root   1675 Dec  6 09:13 front-proxy-ca.key
-rw-r--r-- 1 root root   1119 Dec  6 09:13 front-proxy-client.crt
-rw------- 1 root root   1679 Dec  6 09:13 front-proxy-client.key
-rw------- 1 root root   1679 Dec  6 09:13 sa.key
-rw------- 1 root root    451 Dec  6 09:13 sa.pub
controlplane $ 
controlplane $ 



controlplane $ cd /etc/kube
kube-bench/ kubernetes/ 
controlplane $ cd /etc/kubernetes/
controlplane $ ls
admin.conf  controller-manager.conf  kubelet.conf  manifests  pki  scheduler.conf  super-admin.conf
controlplane $ ls -ltr
total 44
drwxr-xr-x 3 root ubuntu 4096 Dec  6 09:13 pki
-rw------- 1 root root   5654 Dec  6 09:13 admin.conf
-rw------- 1 root root   5678 Dec  6 09:13 super-admin.conf
-rw------- 1 root root   5678 Dec  6 09:13 controller-manager.conf
-rw------- 1 root root   5626 Dec  6 09:13 scheduler.conf
-rw------- 1 root root   1990 Dec  6 09:14 kubelet.conf
drwxrwxr-x 2 root root   4096 Dec 19 11:50 manifests
controlplane $ 
controlplane $ 
controlplane $ chown -R root:root pki/
controlplane $ ls -ltr
total 44
drwxr-xr-x 3 root root 4096 Dec  6 09:13 pki
-rw------- 1 root root 5654 Dec  6 09:13 admin.conf
-rw------- 1 root root 5678 Dec  6 09:13 super-admin.conf
-rw------- 1 root root 5678 Dec  6 09:13 controller-manager.conf
-rw------- 1 root root 5626 Dec  6 09:13 scheduler.conf
-rw------- 1 root root 1990 Dec  6 09:14 kubelet.conf
drwxrwxr-x 2 root root 4096 Dec 19 11:50 manifests
controlplane $ 


########################################################################################



Use context: kubectl config use-context infra-prod

You're ask to evaluate specific settings of cluster2 against the CIS Benchmark recommendations. Use the tool kube-bench which is already installed on the nodes.

Connect using ssh cluster2-controlplane1 and ssh cluster2-node1.

On the master node ensure (correct if necessary) that the CIS recommendations are set for:

The --profiling argument of the kube-controller-manager

The ownership of directory /var/lib/etcd

On the worker node ensure (correct if necessary) that the CIS recommendations are set for:

The permissions of the kubelet configuration /var/lib/kubelet/config.yaml
The --client-ca-file argument of the kubelet




soln

controlplane $ kube-bench run --targets=master | grep kube-controller -A4
1.3.1 Edit the Controller Manager pod specification file /etc/kubernetes/manifests/kube-controller-manager.yaml
on the master node and set the --terminated-pod-gc-threshold to an appropriate threshold,
for example:
--terminated-pod-gc-threshold=10

1.3.2 Edit the Controller Manager pod specification file /etc/kubernetes/manifests/kube-controller-manager.yaml
on the master node and set the below parameter.
--profiling=false

1.4.1 Edit the Scheduler pod specification file /etc/kubernetes/manifests/kube-scheduler.yaml file
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets=master | grep kube-controller -A6
1.3.1 Edit the Controller Manager pod specification file /etc/kubernetes/manifests/kube-controller-manager.yaml
on the master node and set the --terminated-pod-gc-threshold to an appropriate threshold,
for example:
--terminated-pod-gc-threshold=10

1.3.2 Edit the Controller Manager pod specification file /etc/kubernetes/manifests/kube-controller-manager.yaml
on the master node and set the below parameter.
--profiling=false

1.4.1 Edit the Scheduler pod specification file /etc/kubernetes/manifests/kube-scheduler.yaml file
on the master node and set the below parameter.
--profiling=false
controlplane $ vi /etc/kubernetes/manifests/kube-controller-manager.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets master | grep etcd -A4
[PASS] 1.1.7 Ensure that the etcd pod specification file permissions are set to 644 or more restrictive (Automated)
[PASS] 1.1.8 Ensure that the etcd pod specification file ownership is set to root:root (Automated)
[WARN] 1.1.9 Ensure that the Container Network Interface file permissions are set to 644 or more restrictive (Manual)
[PASS] 1.1.10 Ensure that the Container Network Interface file ownership is set to root:root (Manual)
[PASS] 1.1.11 Ensure that the etcd data directory permissions are set to 700 or more restrictive (Automated)
[FAIL] 1.1.12 Ensure that the etcd data directory ownership is set to etcd:etcd (Automated)
[PASS] 1.1.13 Ensure that the admin.conf file permissions are set to 644 or more restrictive (Automated)
[PASS] 1.1.14 Ensure that the admin.conf file ownership is set to root:root (Automated)
[PASS] 1.1.15 Ensure that the scheduler.conf file permissions are set to 644 or more restrictive (Automated)
[PASS] 1.1.16 Ensure that the scheduler.conf file ownership is set to root:root (Automated)
--
[PASS] 1.2.28 Ensure that the --etcd-certfile and --etcd-keyfile arguments are set as appropriate (Automated)
[PASS] 1.2.29 Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate (Automated)
[PASS] 1.2.30 Ensure that the --client-ca-file argument is set as appropriate (Automated)
[PASS] 1.2.31 Ensure that the --etcd-cafile argument is set as appropriate (Automated)
[WARN] 1.2.32 Ensure that the --encryption-provider-config argument is set as appropriate (Manual)
[WARN] 1.2.33 Ensure that encryption providers are appropriately configured (Manual)
[WARN] 1.2.34 Ensure that the API Server only makes use of Strong Cryptographic Ciphers (Manual)
[INFO] 1.3 Controller Manager
--
1.1.12 On the etcd server node, get the etcd data directory, passed as an argument --data-dir,
from the below command:
ps -ef | grep etcd
Run the below command (based on the etcd data directory found above).
For example, chown etcd:etcd /var/lib/etcd

1.1.19 Run the below command (based on the file location on your system) on the master node.
For example,
chown -R root:root /etc/kubernetes/pki/
controlplane $ 
controlplane $ kube-bench run --targets master --check 1.1.12 
[INFO] 1 Master Node Security Configuration
[INFO] 1.1 Master Node Configuration Files
[FAIL] 1.1.12 Ensure that the etcd data directory ownership is set to etcd:etcd (Automated)

== Remediations master ==
1.1.12 On the etcd server node, get the etcd data directory, passed as an argument --data-dir,
from the below command:
ps -ef | grep etcd
Run the below command (based on the etcd data directory found above).
For example, chown etcd:etcd /var/lib/etcd


== Summary master ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

== Summary total ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ll /var/lib/etcd
total 12
drwx------  3 root root 4096 Dec 19 11:47 ./
drwxr-xr-x 71 root root 4096 Dec  6 09:20 ../
drwx------  4 root root 4096 Dec 19 11:47 member/
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ll /var/lib/    
total 284
drwxr-xr-x 71 root      root      4096 Dec  6 09:20 ./
drwxr-xr-x 13 root      root      4096 Nov  7  2022 ../
drwxr-xr-x  4 root      root      4096 Nov  7  2022 AccountsService/
drwx------  2 root      root      4096 Dec  6 09:20 NetworkManager/
drwxr-xr-x  2 root      root      4096 Nov 13  2022 PackageKit/
drwxr-xr-x  3 root      root      4096 Nov 13  2022 apport/
drwxr-xr-x  5 root      root      4096 Dec  6 09:17 apt/
drwxr-xr-x  2 root      root      4096 Dec  6 09:21 aspell/
drwxr-xr-x  2 root      root      4096 Jun  5  2024 bluetooth/
drwxr-xr-x  2 root      root      4096 Feb 25  2022 boltd/
drwxr-xr-x  2 root      root      4096 Dec  6 09:14 calico/
drwxr-xr-x  8 root      root      4096 Nov 13  2022 cloud/
drwxr-xr-x  4 root      root      4096 Dec  6 09:14 cni/
drwxr-xr-x  4 colord    colord    4096 Dec 19 11:47 colord/
drwxr-xr-x  2 root      root      4096 Dec  6 09:05 command-not-found/
drwx--x--x 13 root      root      4096 Dec  6 09:13 containerd/
drwxr-xr-x  3 root      root      4096 Dec  6 09:06 containers/
drwxr-xr-x  2 root      root      4096 Nov 13  2022 dbus/
drwxr-xr-x  2 root      root      4096 Dec  6 09:12 dhcp/
drwxr-xr-x  5 root      root      4096 Dec  6 09:18 dictionaries-common/
drwxr-xr-x  2 root      root      4096 Dec  6 09:06 dkms/
drwx--x--- 12 root      root      4096 Dec 19 11:47 docker/
drwxr-xr-x  7 root      root      4096 Dec 19 12:00 dpkg/
drwxr-xr-x  3 root      root      4096 Dec  6 09:17 emacsen-common/
drwx------  3 root      root      4096 Dec 19 11:47 etcd/
drwxr-xr-x  2 root      root      4096 Feb 22  2021 fprint/
drwxr-xr-x  7 root      root      4096 Dec  6 09:20 fwupd/
drwxr-xr-x  5 gdm       gdm       4096 Dec 19 11:47 gdm3/
drwxr-xr-x  2 geoclue   geoclue   4096 Feb 28  2020 geoclue/
drwxr-xr-x  4 root      root      4096 Dec  6 09:17 ghostscript/
drwxr-xr-x  2 root      root      4096 Oct 13  2022 git/
drwxr-xr-x  4 root      root      4096 Nov  7  2022 grub/
drwxr-xr-x  2 root      root      4096 Dec  6 09:18 ieee-data/
drwxr-xr-x  2 root      root      4096 Nov  7  2022 initramfs-tools/
drwxr-xr-x  2 root      root      4096 Dec  6 09:17 ispell/
drwxrwxr-x  9 root      root      4096 Dec  6 09:13 kubelet/
drwxr-xr-x  2 landscape landscape 4096 Nov  7  2022 landscape/
drwxr-x---  2 lightdm   lightdm   4096 Dec  6 09:20 lightdm/
drwxr-xr-x  2 root      root      4096 Nov  5  2021 lightdm-data/
drwxr-xr-x  2 root      root      4096 Dec 19 11:47 logrotate/
drwxr-xr-x  2 root      root      4096 Nov  7  2022 man-db/
drwxr-xr-x  2 root      root      4096 Apr 15  2020 misc/
drwxr-xr-x  2 root      root      4096 Jun  5  2019 os-prober/
drwxr-xr-x  2 root      root      4096 Dec  6 09:20 pam/
drwxr-xr-x  4 root      root      4096 Dec  6 09:07 php/
drwxr-xr-x  2 root      root      4096 Nov  2  2020 plymouth/
drwx------  3 root      root      4096 Nov  7  2022 polkit-1/
drwx------  2 root      root      4096 Nov  7  2022 private/
drwxr-xr-x  2 root      root      4096 Nov  7  2022 python/
drwxr-xr-x  2 root      root      4096 Dec  6 09:21 sgml-base/
drwxr-xr-x  3 root      root      4096 Nov  7  2022 shim-signed/
drwxr-xr-x 24 root      root      4096 Dec 19 11:57 snapd/
drwxr-xr-x  2 root      root      4096 Jul 28  2023 snmp/
drwxr-xr-x  3 root      root      4096 Nov  7  2022 sudo/
drwxr-xr-x  9 root      root      4096 Nov 13  2022 systemd/
drwxr-xr-x  2 tss       tss       4096 Dec  3  2019 tpm/
drwxr-xr-x  4 root      root      4096 Dec  6 09:19 ubuntu-advantage/
drwxr-xr-x  3 root      root      4096 Dec  6 09:06 ubuntu-fan/
drwxr-xr-x  2 root      root      4096 Aug 19  2022 ubuntu-release-upgrader/
drwxr-xr-x  3 root      root      4096 Dec  6 09:21 ucf/
drwx------  2 root      root      4096 Nov 13  2022 udisks2/
drwxr-xr-x  2 root      root      4096 May 19  2022 unattended-upgrades/
drwxr-xr-x  2 root      root      4096 Jan 14  2022 update-manager/
drwxr-xr-x  4 root      root      4096 Dec 19 11:48 update-notifier/
drwxr-xr-x  2 root      root      4096 Dec 10  2019 upower/
drwxr-xr-x  2 root      root      4096 Feb 10  2020 usb_modeswitch/
drwxr-xr-x  2 root      root      4096 Nov  7  2022 usbutils/
drwxr-xr-x  3 root      root      4096 Nov  7  2022 vim/
drwxr-xr-x  2 root      root      4096 Dec  6 09:20 xfonts/
drwxr-xr-x  2 root      root      4096 Dec 19 11:47 xkb/
drwxr-xr-x  2 root      root      4096 Dec  6 09:21 xml-core/
controlplane $ chown etcd:etcd /var/lib/etcd
chown: invalid user: 'etcd:etcd'
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ chown etcd:etcd /var/lib/etcd
chown: invalid user: 'etcd:etcd'
controlplane $ 
controlplane $ 
controlplane $ adduser etcd 
Adding user `etcd' ...
Adding new group `etcd' (1001) ...
Adding new user `etcd' (1001) with group `etcd' ...
Creating home directory `/home/etcd' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
No password supplied
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for etcd
Enter the new value, or press ENTER for the default
        Full Name []: 
        Room Number []: 
        Work Phone []: 
        Home Phone []: 
        Other []: 
Is the information correct? [Y/n] y
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ chown etcd:etcd /var/lib/etcd
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ll /var/lib/etcd
total 12
drwx------  3 etcd etcd 4096 Dec 19 11:47 ./
drwxr-xr-x 71 root root 4096 Dec  6 09:20 ../
drwx------  4 root root 4096 Dec 19 11:47 member/
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets master --check 1.1.12
[INFO] 1 Master Node Security Configuration
[INFO] 1.1 Master Node Configuration Files
[PASS] 1.1.12 Ensure that the etcd data directory ownership is set to etcd:etcd (Automated)

== Summary master ==
1 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

== Summary total ==
1 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets master |  grep kubelet
[PASS] 1.2.3 Ensure that the --kubelet-https argument is set to true (Automated)
[PASS] 1.2.4 Ensure that the --kubelet-client-certificate and --kubelet-client-key arguments are set as appropriate (Automated)
[FAIL] 1.2.5 Ensure that the --kubelet-certificate-authority argument is set as appropriate (Automated)
the apiserver and kubelets. Then, edit the API server pod specification file
--kubelet-certificate-authority parameter to the path to the cert file for the certificate authority.
--kubelet-certificate-authority=<ca-string>
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets master --check 1.2.5  
[INFO] 1 Master Node Security Configuration
[INFO] 1.2 API Server
[FAIL] 1.2.5 Ensure that the --kubelet-certificate-authority argument is set as appropriate (Automated)

== Remediations master ==
1.2.5 Follow the Kubernetes documentation and setup the TLS connection between
the apiserver and kubelets. Then, edit the API server pod specification file
/etc/kubernetes/manifests/kube-apiserver.yaml on the master node and set the
--kubelet-certificate-authority parameter to the path to the cert file for the certificate authority.
--kubelet-certificate-authority=<ca-string>


== Summary master ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

== Summary total ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd /etc/kubernetes/pki/
controlplane $ ls
apiserver-etcd-client.crt  apiserver-kubelet-client.crt  apiserver.crt  ca.crt  etcd                front-proxy-ca.key      front-proxy-client.key  sa.pub
apiserver-etcd-client.key  apiserver-kubelet-client.key  apiserver.key  ca.key  front-proxy-ca.crt  front-proxy-client.crt  sa.key
controlplane $ ls | grep kubelet
apiserver-kubelet-client.crt
apiserver-kubelet-client.key
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ll /var/lib/kubelet/config.yaml
-rw-r--r-- 1 root root 1102 Dec  6 09:13 /var/lib/kubelet/config.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /var/lib/kubelet/config.yaml
controlplane $ kube-bench run --targets=node | grep /var/lib/kubelet/config.yaml -B2

controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /var/lib/kubelet/config.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /etc/kube   
kube-bench/ kubernetes/ 
controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets=node | grep /var/lib/kubelet/config.yaml -B2
Warning: Kubernetes version was not auto-detected because kubectl could not connect to the Kubernetes server. This may be because the kubeconfig information is missing or has credentials that do not match the server. Assuming default version 1.18
Warning: Kubernetes version was not auto-detected because kubectl could not connect to the Kubernetes server. This may be because the kubeconfig information is missing or has credentials that do not match the server. Assuming default version 1.18
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kube-bench run --targets master --check 1.2.5
Warning: Kubernetes version was not auto-detected because kubectl could not connect to the Kubernetes server. This may be because the kubeconfig information is missing or has credentials that do not match the server. Assuming default version 1.18
Warning: Kubernetes version was not auto-detected because kubectl could not connect to the Kubernetes server. This may be because the kubeconfig information is missing or has credentials that do not match the server. Assuming default version 1.18
[INFO] 1 Master Node Security Configuration
[INFO] 1.2 API Server
[PASS] 1.2.5 Ensure that the --kubelet-client-certificate and --kubelet-client-key arguments are set as appropriate (Automated)

== Summary master ==
1 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

== Summary total ==
1 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
8df096594dfd3       604f5db92eaa8       1 second ago        Running             kube-apiserver            0                   d13a25acef471       kube-apiserver-controlplane
4041027a09ef9       1766f54c897f0       27 seconds ago      Running             kube-scheduler            2                   3dca87659ec1d       kube-scheduler-controlplane
3cb09a3c6f4e1       045733566833c       27 seconds ago      Running             kube-controller-manager   1                   69b23e3cb67a3       kube-controller-manager-controlplane
e3fe8f2ce4ce8       95fef08b8bf89       27 minutes ago      Running             local-path-provisioner    1                   104acde9d9d7e       local-path-provisioner-6c5cff8948-phnkg
a7e9f8f4de926       f9c3c1813269c       27 minutes ago      Running             calico-kube-controllers   1                   bf21a36b3af09       calico-kube-controllers-94fb6bc47-wr56s
b14f57abc424c       cbb01a7bd410d       27 minutes ago      Running             coredns                   1                   579255b1925c2       coredns-57888bfdc7-p24nh
c2123f3cb45fc       cbb01a7bd410d       27 minutes ago      Running             coredns                   1                   b9ff4afc83237       coredns-57888bfdc7-j9ddk
fa7d11c563b96       e6ea68648f0cd       28 minutes ago      Running             kube-flannel              1                   d529dadc43e0e       canal-cdcf7
5d4f0557e68ba       75392e3500e36       28 minutes ago      Running             calico-node               1                   d529dadc43e0e       canal-cdcf7
9ea44b4302fdb       ad83b2ca7b09e       28 minutes ago      Running             kube-proxy                1                   ba9157f98376f       kube-proxy-bt2pv
c21ddcbe35aca       2e96e5913fc06       28 minutes ago      Running             etcd                      1                   347dbcf7f0d27       etcd-controlplane
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   0/1     Running   1 (28m ago)   13d
canal-cdcf7                               2/2     Running   2 (28m ago)   13d
coredns-57888bfdc7-j9ddk                  1/1     Running   1 (28m ago)   13d
coredns-57888bfdc7-p24nh                  1/1     Running   1 (28m ago)   13d
etcd-controlplane                         1/1     Running   1 (28m ago)   13d
kube-apiserver-controlplane               0/1     Pending   0             2s
kube-controller-manager-controlplane      1/1     Running   1 (32s ago)   11m
kube-proxy-bt2pv                          1/1     Running   1 (28m ago)   13d
kube-scheduler-controlplane               1/1     Running   2 (32s ago)   13d
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   0/1     Running   1 (28m ago)   13d
canal-cdcf7                               2/2     Running   2 (28m ago)   13d
coredns-57888bfdc7-j9ddk                  1/1     Running   1 (28m ago)   13d
coredns-57888bfdc7-p24nh                  1/1     Running   1 (28m ago)   13d
etcd-controlplane                         1/1     Running   1 (28m ago)   13d
kube-apiserver-controlplane               0/1     Pending   0             3s
kube-controller-manager-controlplane      1/1     Running   1 (33s ago)   11m
kube-proxy-bt2pv                          1/1     Running   1 (28m ago)   13d
kube-scheduler-controlplane               1/1     Running   2 (33s ago)   13d
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   0/1     Running   1 (28m ago)   13d
canal-cdcf7                               2/2     Running   2 (28m ago)   13d
coredns-57888bfdc7-j9ddk                  1/1     Running   1 (28m ago)   13d
coredns-57888bfdc7-p24nh                  1/1     Running   1 (28m ago)   13d
etcd-controlplane                         1/1     Running   1 (28m ago)   13d
kube-apiserver-controlplane               0/1     Pending   0             6s
kube-controller-manager-controlplane      1/1     Running   1 (36s ago)   11m
kube-proxy-bt2pv                          1/1     Running   1 (28m ago)   13d
kube-scheduler-controlplane               1/1     Running   2 (36s ago)   13d
controlplane $ k delete pod kube-apiserver-controlplane -n kube-system
pod "kube-apiserver-controlplane" deleted
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   1 (29m ago)   13d
canal-cdcf7                               2/2     Running   2 (29m ago)   13d
coredns-57888bfdc7-j9ddk                  1/1     Running   1 (29m ago)   13d
coredns-57888bfdc7-p24nh                  1/1     Running   1 (29m ago)   13d
etcd-controlplane                         1/1     Running   1 (29m ago)   13d
kube-apiserver-controlplane               1/1     Running   0             2s
kube-controller-manager-controlplane      1/1     Running   1 (53s ago)   11m
kube-proxy-bt2pv                          1/1     Running   1 (29m ago)   13d
kube-scheduler-controlplane               1/1     Running   2 (53s ago)   13d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   1 (29m ago)   13d
canal-cdcf7                               2/2     Running   2 (29m ago)   13d
coredns-57888bfdc7-j9ddk                  1/1     Running   1 (29m ago)   13d
coredns-57888bfdc7-p24nh                  1/1     Running   1 (29m ago)   13d
etcd-controlplane                         1/1     Running   1 (29m ago)   13d
kube-apiserver-controlplane               1/1     Running   0             5s
kube-controller-manager-controlplane      1/1     Running   1 (56s ago)   11m
kube-proxy-bt2pv                          1/1     Running   1 (29m ago)   13d
kube-scheduler-controlplane               1/1     Running   2 (56s ago)   13d
controlplane $ 
controlplane $ 

