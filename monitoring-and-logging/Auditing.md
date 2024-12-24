# create audit policy for api server 

apiVersion: audit.k8s.io/v1
kind: Policy
rules:
- level: Metadata






controlplane $ k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   11d   v1.31.0
node01         Ready    <none>          11d   v1.31.0
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd /etc/kubernetes/
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ mkdir audit
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ls -ltr
total 48
drwxr-xr-x 3 root root 4096 Dec  6 09:13 pki
-rw------- 1 root root 5654 Dec  6 09:13 admin.conf
-rw------- 1 root root 5678 Dec  6 09:13 super-admin.conf
-rw------- 1 root root 5678 Dec  6 09:13 controller-manager.conf
-rw------- 1 root root 5626 Dec  6 09:13 scheduler.conf
-rw------- 1 root root 1990 Dec  6 09:14 kubelet.conf
drwxrwxr-x 2 root root 4096 Dec  6 09:15 manifests
drwxr-xr-x 2 root root 4096 Dec 18 04:54 audit
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd audit/
controlplane $ vi policy.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ pwd
/etc/kubernetes/audit
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
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
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
c314857b729f4       1766f54c897f0       5 seconds ago       Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       5 seconds ago       Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
888342790670e       f9c3c1813269c       54 minutes ago      Running             calico-kube-controllers   2                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
455db532c9e7b       95fef08b8bf89       54 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       55 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       55 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       55 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       56 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
1c7cdd4c4a5f8       604f5db92eaa8       56 minutes ago      Running             kube-apiserver            2                   e39e5a408faca       kube-apiserver-controlplane
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
c314857b729f4       1766f54c897f0       8 seconds ago       Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       8 seconds ago       Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
888342790670e       f9c3c1813269c       54 minutes ago      Running             calico-kube-controllers   2                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
455db532c9e7b       95fef08b8bf89       55 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       55 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       55 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       55 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       56 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
1c7cdd4c4a5f8       604f5db92eaa8       56 minutes ago      Running             kube-apiserver            2                   e39e5a408faca       kube-apiserver-controlplane
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
c314857b729f4       1766f54c897f0       13 seconds ago      Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       13 seconds ago      Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
888342790670e       f9c3c1813269c       55 minutes ago      Running             calico-kube-controllers   2                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
455db532c9e7b       95fef08b8bf89       55 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       55 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       55 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       55 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       56 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
1c7cdd4c4a5f8       604f5db92eaa8       56 minutes ago      Running             kube-apiserver            2                   e39e5a408faca       kube-apiserver-controlplane
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
c314857b729f4       1766f54c897f0       15 seconds ago      Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       15 seconds ago      Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
888342790670e       f9c3c1813269c       55 minutes ago      Running             calico-kube-controllers   2                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
455db532c9e7b       95fef08b8bf89       55 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       55 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       55 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       56 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       56 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
1c7cdd4c4a5f8       604f5db92eaa8       56 minutes ago      Running             kube-apiserver            2                   e39e5a408faca       kube-apiserver-controlplane


controlplane $ k get pod -n kube-system,
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ k get pod -n kube-system 
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd /var/log/pods/kube-system_kube-apiserver-controlplane_56ef925343727de7d2558029152c5b5f/
controlplane $ ls
kube-apiserver
controlplane $ cd kube-apiserver/
controlplane $ ls
1.log
controlplane $ cat 1.
cat: 1.: No such file or directory
controlplane $ ls     
2.log
controlplane $ 
controlplane $ 
controlplane $ cat 2.log 
2024-12-18T05:05:02.815405732Z stderr F I1218 05:05:02.806450       1 options.go:228] external host was not specified, using 172.30.1.2
2024-12-18T05:05:02.815465464Z stderr F I1218 05:05:02.813717       1 server.go:142] Version: v1.31.0
2024-12-18T05:05:02.815471662Z stderr F I1218 05:05:02.813759       1 server.go:144] "Golang settings" GOGC="" GOMAXPROCS="" GOTRACEBACK=""
2024-12-18T05:05:03.206280924Z stderr F E1218 05:05:03.206099       1 run.go:72] "command failed" err="loading audit policy file: failed to read file path \"/etc/kubernetes/policy.yaml\": open /etc/kubernetes/policy.yaml: no such file or directory"
controlplane $ 
controlplane $ 

controlplane $ 
controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ls
3.log
controlplane $ cat 3.log 
2024-12-18T05:05:34.56522141Z stderr F I1218 05:05:34.565060       1 options.go:228] external host was not specified, using 172.30.1.2
2024-12-18T05:05:34.567380948Z stderr F I1218 05:05:34.567195       1 server.go:142] Version: v1.31.0
2024-12-18T05:05:34.567551603Z stderr F I1218 05:05:34.567500       1 server.go:144] "Golang settings" GOGC="" GOMAXPROCS="" GOTRACEBACK=""
2024-12-18T05:05:35.134465472Z stderr F E1218 05:05:35.130706       1 run.go:72] "command failed" err="loading audit policy file: failed to read file path \"/etc/kubernetes/policy.yaml\": open /etc/kubernetes/policy.yaml: no such file or directory"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat 3.log 
2024-12-18T05:05:34.56522141Z stderr F I1218 05:05:34.565060       1 options.go:228] external host was not specified, using 172.30.1.2
2024-12-18T05:05:34.567380948Z stderr F I1218 05:05:34.567195       1 server.go:142] Version: v1.31.0
2024-12-18T05:05:34.567551603Z stderr F I1218 05:05:34.567500       1 server.go:144] "Golang settings" GOGC="" GOMAXPROCS="" GOTRACEBACK=""
2024-12-18T05:05:35.134465472Z stderr F E1218 05:05:35.130706       1 run.go:72] "command failed" err="loading audit policy file: failed to read file path \"/etc/kubernetes/policy.yaml\": open /etc/kubernetes/policy.yaml: no such file or directory"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED              STATE               NAME                      ATTEMPT             POD ID              POD
c314857b729f4       1766f54c897f0       About a minute ago   Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       About a minute ago   Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
455db532c9e7b       95fef08b8bf89       56 minutes ago       Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       56 minutes ago       Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       56 minutes ago       Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       57 minutes ago       Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       57 minutes ago       Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED                  STATE               NAME                      ATTEMPT             POD ID              POD
6a8288d8a4694       604f5db92eaa8       Less than a second ago   Running             kube-apiserver            1                   d220275f7fd5c       kube-apiserver-controlplane
c314857b729f4       1766f54c897f0       About a minute ago       Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       About a minute ago       Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
455db532c9e7b       95fef08b8bf89       56 minutes ago           Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       56 minutes ago           Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       56 minutes ago           Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       57 minutes ago           Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       57 minutes ago           Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
controlplane $ 
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
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED                  STATE               NAME                      ATTEMPT             POD ID              POD
31aa320131892       f9c3c1813269c       Less than a second ago   Running             calico-kube-controllers   4                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
c314857b729f4       1766f54c897f0       2 minutes ago            Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       2 minutes ago            Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
455db532c9e7b       95fef08b8bf89       57 minutes ago           Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       57 minutes ago           Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       57 minutes ago           Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       57 minutes ago           Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       58 minutes ago           Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
31aa320131892       f9c3c1813269c       3 seconds ago       Running             calico-kube-controllers   4                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
c314857b729f4       1766f54c897f0       2 minutes ago       Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       2 minutes ago       Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
455db532c9e7b       95fef08b8bf89       57 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       57 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       57 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       58 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       58 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ls
3.log
controlplane $ cat 3.log 
2024-12-18T05:05:34.56522141Z stderr F I1218 05:05:34.565060       1 options.go:228] external host was not specified, using 172.30.1.2
2024-12-18T05:05:34.567380948Z stderr F I1218 05:05:34.567195       1 server.go:142] Version: v1.31.0
2024-12-18T05:05:34.567551603Z stderr F I1218 05:05:34.567500       1 server.go:144] "Golang settings" GOGC="" GOMAXPROCS="" GOTRACEBACK=""
2024-12-18T05:05:35.134465472Z stderr F E1218 05:05:35.130706       1 run.go:72] "command failed" err="loading audit policy file: failed to read file path \"/etc/kubernetes/policy.yaml\": open /etc/kubernetes/policy.yaml: no such file or directory"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
8b6d3b39b5784       f9c3c1813269c       13 seconds ago      Running             calico-kube-controllers   5                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
c314857b729f4       1766f54c897f0       2 minutes ago       Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       2 minutes ago       Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
455db532c9e7b       95fef08b8bf89       57 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       57 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       57 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       58 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       58 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
controlplane $ ls
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
8b6d3b39b5784       f9c3c1813269c       31 seconds ago      Running             calico-kube-controllers   5                   0b1e49bb1a69c       calico-kube-controllers-94fb6bc47-wr56s
c314857b729f4       1766f54c897f0       2 minutes ago       Running             kube-scheduler            3                   56ec0f2d46dc4       kube-scheduler-controlplane
d5f70a95b63e5       045733566833c       2 minutes ago       Running             kube-controller-manager   3                   76eb16f7e3ac5       kube-controller-manager-controlplane
455db532c9e7b       95fef08b8bf89       57 minutes ago      Running             local-path-provisioner    2                   771d6de308376       local-path-provisioner-6c5cff8948-phnkg
8cde2132f8db6       e6ea68648f0cd       57 minutes ago      Running             kube-flannel              1                   488803ca69bf7       canal-cgrhr
669ca7a25b648       75392e3500e36       57 minutes ago      Running             calico-node               1                   488803ca69bf7       canal-cgrhr
aa706b0f0acb0       ad83b2ca7b09e       58 minutes ago      Running             kube-proxy                2                   4335932a16a56       kube-proxy-bt2pv
0c2050f62064a       2e96e5913fc06       58 minutes ago      Running             etcd                      2                   8dc37e60aa658       etcd-controlplane
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd /var/log/syslog
bash: cd: /var/log/syslog: Not a directory
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ tail /var/log/syslog
Dec 18 05:07:38 controlplane kubelet[1601]: I1218 05:07:38.368732    1601 scope.go:117] "RemoveContainer" containerID="52898acfecdf4575c83fb8e080420476ae8111d528392a17a5bb382db6345406"
Dec 18 05:07:38 controlplane kubelet[1601]: E1218 05:07:38.369359    1601 pod_workers.go:1301] "Error syncing pod, skipping" err="failed to \"StartContainer\" for \"kube-apiserver\" with CrashLoopBackOff: \"back-off 1m20s restarting failed container=kube-apiserver pod=kube-apiserver-controlplane_kube-system(d94a64571656de62caa0f053db9a3b52)\"" pod="kube-system/kube-apiserver-controlplane" podUID="d94a64571656de62caa0f053db9a3b52"
Dec 18 05:07:38 controlplane kubelet[1601]: E1218 05:07:38.787419    1601 event.go:368] "Unable to write event (may retry after sleeping)" err="Patch \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/events/kube-scheduler-controlplane.181229e9742664b6\": dial tcp 172.30.1.2:6443: connect: connection refused" event="&Event{ObjectMeta:{kube-scheduler-controlplane.181229e9742664b6  kube-system   1886 0 0001-01-01 00:00:00 +0000 UTC <nil> <nil> map[] map[] [] [] []},InvolvedObject:ObjectReference{Kind:Pod,Namespace:kube-system,Name:kube-scheduler-controlplane,UID:0cfa7f19a2c8cf4c1add14122593c823,APIVersion:v1,ResourceVersion:,FieldPath:spec.containers{kube-scheduler},},Reason:Pulled,Message:Container image \"registry.k8s.io/kube-scheduler:v1.31.0\" already present on machine,Source:EventSource{Component:kubelet,Host:controlplane,},FirstTimestamp:2024-12-18 04:08:09 +0000 UTC,LastTimestamp:2024-12-18 05:04:09.778723313 +0000 UTC m=+3363.130859639,Count:2,Type:Normal,EventTime:0001-01-01 00:00:00 +0000 UTC,Series:nil,Action:,Related:nil,ReportingController:kubelet,ReportingInstance:controlplane,}"
Dec 18 05:07:42 controlplane systemd[1]: run-containerd-runc-k8s.io-669ca7a25b64808fecd7759839bd4a3f4947c28eb3352d329f898e031bc1f9b1-runc.YDYFY2.mount: Succeeded.
Dec 18 05:07:42 controlplane systemd[807]: run-containerd-runc-k8s.io-669ca7a25b64808fecd7759839bd4a3f4947c28eb3352d329f898e031bc1f9b1-runc.YDYFY2.mount: Succeeded.
Dec 18 05:07:42 controlplane systemd[1]: run-containerd-runc-k8s.io-1d4d18dc4344098645940cdff57a8c8f422a97eec0cc9bd2b3c68f6ddd163fa1-runc.WRVH0Q.mount: Succeeded.
Dec 18 05:07:42 controlplane systemd[1]: run-containerd-runc-k8s.io-1d4d18dc4344098645940cdff57a8c8f422a97eec0cc9bd2b3c68f6ddd163fa1-runc.Zw3nZ6.mount: Succeeded.
Dec 18 05:07:42 controlplane systemd[807]: run-containerd-runc-k8s.io-1d4d18dc4344098645940cdff57a8c8f422a97eec0cc9bd2b3c68f6ddd163fa1-runc.WRVH0Q.mount: Succeeded.
Dec 18 05:07:42 controlplane systemd[807]: run-containerd-runc-k8s.io-1d4d18dc4344098645940cdff57a8c8f422a97eec0cc9bd2b3c68f6ddd163fa1-runc.Zw3nZ6.mount: Succeeded.
Dec 18 05:07:42 controlplane containerd[691]: time="2024-12-18T05:07:42.284028064Z" level=info msg="StopPodSandbox for \"6c04d78e8beb3175dc33a20b225f6e194f06f70ef31875e1df31051b6c9ae095\""
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ tail /var/log/syslog
Dec 18 05:09:03 controlplane kubelet[1601]: E1218 05:09:03.521269    1601 mirror_client.go:138] "Failed deleting a mirror pod" err="Delete \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-apiserver-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused" pod="kube-system/kube-apiserver-controlplane"
Dec 18 05:09:03 controlplane kubelet[1601]: I1218 05:09:03.521847    1601 status_manager.go:851] "Failed to get status for pod" podUID="a55d9c391dc5f492555b54cdef44652d" pod="kube-system/kube-controller-manager-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-controller-manager-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 18 05:09:03 controlplane kubelet[1601]: I1218 05:09:03.523846    1601 status_manager.go:851] "Failed to get status for pod" podUID="33dc4a2d-9449-4b80-ae4e-09237c0e3188" pod="kube-system/calico-kube-controllers-94fb6bc47-wr56s" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/calico-kube-controllers-94fb6bc47-wr56s\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 18 05:09:03 controlplane kubelet[1601]: I1218 05:09:03.524399    1601 status_manager.go:851] "Failed to get status for pod" podUID="0cfa7f19a2c8cf4c1add14122593c823" pod="kube-system/kube-scheduler-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-scheduler-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 18 05:09:04 controlplane systemd[1]: cri-containerd-5991722d9ec687dc6ae70c6666dad1fe6a6734de63876deea17c436ff653bdd9.scope: Succeeded.
Dec 18 05:09:04 controlplane systemd[1]: run-containerd-io.containerd.runtime.v2.task-k8s.io-5991722d9ec687dc6ae70c6666dad1fe6a6734de63876deea17c436ff653bdd9-rootfs.mount: Succeeded.
Dec 18 05:09:04 controlplane systemd[807]: run-containerd-io.containerd.runtime.v2.task-k8s.io-5991722d9ec687dc6ae70c6666dad1fe6a6734de63876deea17c436ff653bdd9-rootfs.mount: Succeeded.
Dec 18 05:09:04 controlplane containerd[691]: time="2024-12-18T05:09:04.114664918Z" level=info msg="shim disconnected" id=5991722d9ec687dc6ae70c6666dad1fe6a6734de63876deea17c436ff653bdd9 namespace=k8s.io
Dec 18 05:09:04 controlplane containerd[691]: time="2024-12-18T05:09:04.114817644Z" level=warning msg="cleaning up after shim disconnected" id=5991722d9ec687dc6ae70c6666dad1fe6a6734de63876deea17c436ff653bdd9 namespace=k8s.io
Dec 18 05:09:04 controlplane containerd[691]: time="2024-12-18T05:09:04.114827891Z" level=info msg="cleaning up dead shim" namespace=k8s.io
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS             RESTARTS        AGE
calico-kube-controllers-94fb6bc47-wr56s   0/1     CrashLoopBackOff   7 (61s ago)     11d
canal-cgrhr                               2/2     Running            2 (64m ago)     11d
canal-jb5rr                               2/2     Running            2 (64m ago)     11d
coredns-57888bfdc7-895dj                  1/1     Running            1 (64m ago)     11d
coredns-57888bfdc7-9rjt5                  1/1     Running            1 (64m ago)     11d
etcd-controlplane                         1/1     Running            2 (64m ago)     11d
kube-apiserver-controlplane               0/1     Pending            0               34s
kube-controller-manager-controlplane      1/1     Running            3 (7m58s ago)   11d
kube-proxy-5xtp7                          1/1     Running            1 (64m ago)     11d
kube-proxy-bt2pv                          1/1     Running            2 (64m ago)     11d
kube-scheduler-controlplane               1/1     Running            3 (7m58s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k delete pod calico-kube-controllers-94fb6bc47-wr56s -n kube-system
pod "calico-kube-controllers-94fb6bc47-wr56s" deleted
controlplane $ 