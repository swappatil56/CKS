controlplane $ apt-cache madison kubeadm
   kubeadm | 1.31.4-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.3-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.2-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.1-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.0-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apt-mark hold kubelet
kubelet set on hold.
controlplane $ apt-mark hold kubectl
kubectl set on hold.
controlplane $ apt-mark unhold kubeadm
kubeadm was already not hold.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apt-get install kubeadm=1.31.4-1.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be upgraded:
  kubeadm
1 upgraded, 0 newly installed, 0 to remove and 184 not upgraded.
Need to get 11.4 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  kubeadm 1.31.4-1.1 [11.4 MB]
Fetched 11.4 MB in 1s (13.4 MB/s)  
(Reading database ... 132638 files and directories currently installed.)
Preparing to unpack .../kubeadm_1.31.4-1.1_amd64.deb ...
Unpacking kubeadm (1.31.4-1.1) over (1.31.0-1.1) ...
Setting up kubeadm (1.31.4-1.1) ...
controlplane $ 


controlplane $ kubeadm version
kubeadm version: &version.Info{Major:"1", Minor:"31", GitVersion:"v1.31.4", GitCommit:"a78aa47129b8539636eb86a9d00e31b2720fe06b", GitTreeState:"clean", BuildDate:"2024-12-10T11:42:09Z", GoVersion:"go1.22.9", Compiler:"gc", Platform:"linux/amd64"}
controlplane $ 
controlplane $ 
controlplane $ apt-mark hold kubeadm 
kubeadm set on hold.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kubeadm upgrade plan
[preflight] Running pre-flight checks.
[upgrade/config] Reading configuration from the cluster...
[upgrade/config] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -o yaml'
[upgrade] Running cluster health checks
[upgrade] Fetching available versions to upgrade to
[upgrade/versions] Cluster version: 1.31.0
[upgrade/versions] kubeadm version: v1.31.4
I1212 09:30:22.881930   76923 version.go:261] remote version is much newer: v1.32.0; falling back to: stable-1.31
[upgrade/versions] Target version: v1.31.4
[upgrade/versions] Latest version in the v1.31 series: v1.31.4

Components that must be upgraded manually after you have upgraded the control plane with 'kubeadm upgrade apply':
COMPONENT   NODE           CURRENT   TARGET
kubelet     controlplane   v1.31.0   v1.31.4
kubelet     node01         v1.31.0   v1.31.4

Upgrade to the latest version in the v1.31 series:

COMPONENT                 NODE           CURRENT    TARGET
kube-apiserver            controlplane   v1.31.0    v1.31.4
kube-controller-manager   controlplane   v1.31.0    v1.31.4
kube-scheduler            controlplane   v1.31.0    v1.31.4
kube-proxy                               1.31.0     v1.31.4
CoreDNS                                  v1.11.1    v1.11.3
etcd                      controlplane   3.5.15-0   3.5.15-0

You can now apply the upgrade by executing the following command:

        kubeadm upgrade apply v1.31.4

_____________________________________________________________________


The table below shows the current state of component configs as understood by this version of kubeadm.
Configs that have a "yes" mark in the "MANUAL UPGRADE REQUIRED" column require manual config upgrade or
resetting to kubeadm defaults before a successful upgrade can be performed. The version to manually
upgrade to is denoted in the "PREFERRED VERSION" column.

API GROUP                 CURRENT VERSION   PREFERRED VERSION   MANUAL UPGRADE REQUIRED
kubeproxy.config.k8s.io   v1alpha1          v1alpha1            no
kubelet.config.k8s.io     v1beta1           v1beta1             no
_____________________________________________________________________

controlplane $ k get nodes
NAME           STATUS   ROLES           AGE     VERSION
controlplane   Ready    control-plane   6d      v1.31.0
node01         Ready    <none>          5d23h   v1.31.0
controlplane $ 
controlplane $ 


controlplane $ k drain controlplane --ignore-daemonsets
node/controlplane cordoned
Warning: ignoring DaemonSet-managed Pods: kube-system/canal-cgrhr, kube-system/kube-proxy-bt2pv
evicting pod local-path-storage/local-path-provisioner-6c5cff8948-phnkg
evicting pod kube-system/calico-kube-controllers-94fb6bc47-wr56s
pod/local-path-provisioner-6c5cff8948-phnkg evicted
pod/calico-kube-controllers-94fb6bc47-wr56s evicted
node/controlplane drained
controlplane $ 
controlplane $ 
controlplane $ kubeadm upgrade apply v1.31.4
[preflight] Running pre-flight checks.
[upgrade/config] Reading configuration from the cluster...
[upgrade/config] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -o yaml'
[upgrade] Running cluster health checks
[upgrade/version] You have chosen to change the cluster version to "v1.31.4"
[upgrade/versions] Cluster version: v1.31.0
[upgrade/versions] kubeadm version: v1.31.4
[upgrade] Are you sure you want to proceed? [y/N]: y
[upgrade/prepull] Pulling images required for setting up a Kubernetes cluster
[upgrade/prepull] This might take a minute or two, depending on the speed of your internet connection
[upgrade/prepull] You can also perform this action beforehand using 'kubeadm config images pull'
W1212 09:32:33.097812   77965 checks.go:846] detected that the sandbox image "registry.k8s.io/pause:3.5" of the container runtime is inconsistent with that used by kubeadm.It is recommended to use "registry.k8s.io/pause:3.10" as the CRI sandbox image.
[upgrade/apply] Upgrading your Static Pod-hosted control plane to version "v1.31.4" (timeout: 5m0s)...
[upgrade/staticpods] Writing new Static Pod manifests to "/etc/kubernetes/tmp/kubeadm-upgraded-manifests3580891215"
[upgrade/staticpods] Preparing for "etcd" upgrade
[upgrade/staticpods] Renewing etcd-server certificate
[upgrade/staticpods] Renewing etcd-peer certificate
[upgrade/staticpods] Renewing etcd-healthcheck-client certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/etcd.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2024-12-12-09-32-58/etcd.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=etcd
[upgrade/staticpods] Component "etcd" upgraded successfully!
[upgrade/etcd] Waiting for etcd to become available
[upgrade/staticpods] Preparing for "kube-apiserver" upgrade
[upgrade/staticpods] Renewing apiserver certificate
[upgrade/staticpods] Renewing apiserver-kubelet-client certificate
[upgrade/staticpods] Renewing front-proxy-client certificate
[upgrade/staticpods] Renewing apiserver-etcd-client certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/kube-apiserver.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2024-12-12-09-32-58/kube-apiserver.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=kube-apiserver
[upgrade/staticpods] Component "kube-apiserver" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-controller-manager" upgrade
[upgrade/staticpods] Renewing controller-manager.conf certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/kube-controller-manager.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2024-12-12-09-32-58/kube-controller-manager.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=kube-controller-manager
[upgrade/staticpods] Component "kube-controller-manager" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-scheduler" upgrade
[upgrade/staticpods] Renewing scheduler.conf certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/kube-scheduler.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2024-12-12-09-32-58/kube-scheduler.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=kube-scheduler
[upgrade/staticpods] Component "kube-scheduler" upgraded successfully!
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config" in namespace kube-system with the configuration for the kubelets in the cluster
[upgrade] Backing up kubelet config file to /etc/kubernetes/tmp/kubeadm-kubelet-config3076739338/config.yaml
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] Configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] Configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

[upgrade/successful] SUCCESS! Your cluster was upgraded to "v1.31.4". Enjoy!

[upgrade/kubelet] Now that your control plane is upgraded, please proceed with upgrading your kubelets if you haven't already done so.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get nodes
NAME           STATUS                     ROLES           AGE   VERSION
controlplane   Ready,SchedulingDisabled   control-plane   6d    v1.31.0
node01         Ready                      <none>          6d    v1.31.0
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apt-mark hold kubeadm
kubeadm was already set on hold.

controlplane $ apt-mark unhold kubectl
Canceled hold on kubectl.
controlplane $ apt-mark unhold kubelet
Canceled hold on kubelet.
controlplane $ 
controlplane $ 



controlplane $ 
controlplane $ 
controlplane $ apt-cache madison kubeadm     
   kubeadm | 1.31.4-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.3-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.2-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.1-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.0-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apt-get install kubelet=1.31.4-1.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ebtables socat
Use 'apt autoremove' to remove them.
The following packages will be upgraded:
  kubelet
1 upgraded, 0 newly installed, 0 to remove and 183 not upgraded.
Need to get 15.2 MB of archives.
After this operation, 36.9 kB of additional disk space will be used.
Get:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  kubelet 1.31.4-1.1 [15.2 MB]
Fetched 15.2 MB in 1s (23.1 MB/s)
(Reading database ... 132638 files and directories currently installed.)
Preparing to unpack .../kubelet_1.31.4-1.1_amd64.deb ...
Unpacking kubelet (1.31.4-1.1) over (1.31.0-1.1) ...
Setting up kubelet (1.31.4-1.1) ...
controlplane $ apt-get install kubectl=1.31.4-1.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ebtables socat
Use 'apt autoremove' to remove them.
The following packages will be upgraded:
  kubectl
1 upgraded, 0 newly installed, 0 to remove and 182 not upgraded.
Need to get 11.2 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  kubectl 1.31.4-1.1 [11.2 MB]
Fetched 11.2 MB in 1s (14.5 MB/s)
(Reading database ... 132638 files and directories currently installed.)
Preparing to unpack .../kubectl_1.31.4-1.1_amd64.deb ...
Unpacking kubectl (1.31.4-1.1) over (1.31.0-1.1) ...
Setting up kubectl (1.31.4-1.1) ...
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apt-mark hold kubelet
kubelet set on hold.
controlplane $ apt-mark hold kubectl
kubectl set on hold.
controlplane $ service kubelet restart
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ service kubelet status 
● kubelet.service - kubelet: The Kubernetes Node Agent
     Loaded: loaded (/lib/systemd/system/kubelet.service; enabled; vendor preset: enabled)
    Drop-In: /usr/lib/systemd/system/kubelet.service.d
             └─10-kubeadm.conf
     Active: active (running) since Thu 2024-12-12 09:54:45 UTC; 5s ago
       Docs: https://kubernetes.io/docs/
   Main PID: 85147 (kubelet)
      Tasks: 9 (limit: 2338)
     Memory: 60.0M
     CGroup: /system.slice/kubelet.service
             └─85147 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --cont>


controlplane $ kubelet --version
Kubernetes v1.31.4
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get nodes
NAME           STATUS                     ROLES           AGE   VERSION
controlplane   Ready,SchedulingDisabled   control-plane   6d    v1.31.4
node01         Ready                      <none>          6d    v1.31.0

controlplane $ k uncordon controlplane
node/controlplane uncordoned
controlplane $ 
controlplane $ 

controlplane $ k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   6d    v1.31.4
node01         Ready    <none>          6d    v1.31.0

################################################################


controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
node01 $ 
node01 $ 
node01 $ 
node01 $ apt-get update
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://archive.ubuntu.com/ubuntu focal-updates InRelease [128 kB]                                                                                                     
Get:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease [128 kB]                                                                                                   
Get:5 http://security.ubuntu.com/ubuntu focal-security InRelease [128 kB]      
Hit:6 http://ppa.launchpad.net/rmescandon/yq/ubuntu focal InRelease
Hit:3 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  InRelease
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [3684 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [1239 kB]
Fetched 5306 kB in 3s (1928 kB/s)                        
Reading package lists... Done
node01 $ 
node01 $ 
node01 $ 
node01 $ apt-cache madison kubeadm
   kubeadm | 1.31.4-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.3-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.2-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.1-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
   kubeadm | 1.31.0-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
node01 $ apt-mark hold kubelet 
kubelet set on hold.
node01 $ apt-mark hold kubectl 
kubectl set on hold.
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ apt-mark unhold kubeadm
kubeadm was already not hold.
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ apt-get install kubeadm=1.31.4-1.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be upgraded:
  kubeadm
1 upgraded, 0 newly installed, 0 to remove and 185 not upgraded.
Need to get 11.4 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  kubeadm 1.31.4-1.1 [11.4 MB]
Fetched 11.4 MB in 1s (14.3 MB/s)
(Reading database ... 73016 files and directories currently installed.)
Preparing to unpack .../kubeadm_1.31.4-1.1_amd64.deb ...
Unpacking kubeadm (1.31.4-1.1) over (1.31.0-1.1) ...
Setting up kubeadm (1.31.4-1.1) ...
node01 $ 





















node01 $ apt-get install kubelet=1.31.4-1.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ebtables socat
Use 'apt autoremove' to remove them.
The following packages will be upgraded:
  kubelet
1 upgraded, 0 newly installed, 0 to remove and 184 not upgraded.
Need to get 15.2 MB of archives.
After this operation, 36.9 kB of additional disk space will be used.
Get:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  kubelet 1.31.4-1.1 [15.2 MB]
Fetched 15.2 MB in 1s (14.6 MB/s)  
(Reading database ... 73016 files and directories currently installed.)
Preparing to unpack .../kubelet_1.31.4-1.1_amd64.deb ...
Unpacking kubelet (1.31.4-1.1) over (1.31.0-1.1) ...
Setting up kubelet (1.31.4-1.1) ...

node01 $ 
node01 $ apt-get install kubectl=1.31.4-1.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ebtables socat
Use 'apt autoremove' to remove them.
The following packages will be upgraded:
  kubectl
1 upgraded, 0 newly installed, 0 to remove and 183 not upgraded.
Need to get 11.2 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  kubectl 1.31.4-1.1 [11.2 MB]
Fetched 11.2 MB in 1s (15.4 MB/s)
(Reading database ... 73016 files and directories currently installed.)
Preparing to unpack .../kubectl_1.31.4-1.1_amd64.deb ...
Unpacking kubectl (1.31.4-1.1) over (1.31.0-1.1) ...
Setting up kubectl (1.31.4-1.1) ...
node01 $ 