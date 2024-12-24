# /proc directory


- contains information and connections to processes and kernel
- study it and learn how processes works 
- configuration and administrative tasks
- contains files that don't exists , yet you can access these

#####strace Kubernetes etcd

- list syscalls
- find openfiles
- read secret value




controlplane $ crictl ps | grep etcd
03596553c9257       2e96e5913fc06       28 minutes ago      Running             etcd                      2                   f9fa9d6124512       etcd-controlplane
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ps aux | grep etcd
root        1921  1.9  2.9 11737972 60184 ?      Ssl  05:47   0:33 etcd --advertise-client-urls=https://172.30.1.2:2379 --cert-file=/etc/kubernetes/pki/etcd/server.crt --client-cert-auth=true --data-dir=/var/lib/etcd --experimental-initial-corrupt-check=true --experimental-watch-progress-notify-interval=5s --initial-advertise-peer-urls=https://172.30.1.2:2380 --initial-cluster=controlplane=https://172.30.1.2:2380 --key-file=/etc/kubernetes/pki/etcd/server.key --listen-client-urls=https://127.0.0.1:2379,https://172.30.1.2:2379 --listen-metrics-urls=http://127.0.0.1:2381 --listen-peer-urls=https://172.30.1.2:2380 --name=controlplane --peer-cert-file=/etc/kubernetes/pki/etcd/peer.crt --peer-client-cert-auth=true --peer-key-file=/etc/kubernetes/pki/etcd/peer.key --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt --snapshot-count=10000 --trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
root        1976  4.0 12.4 1519132 252672 ?      Ssl  05:47   1:09 kube-apiserver --advertise-address=172.30.1.2 --allow-privileged=true --authorization-mode=Node,RBAC --client-ca-file=/etc/kubernetes/pki/ca.crt --enable-admission-plugins=NodeRestriction --enable-bootstrap-token-auth=true --etcd-cafile=/etc/kubernetes/pki/etcd/ca.crt --etcd-certfile=/etc/kubernetes/pki/apiserver-etcd-client.crt --etcd-keyfile=/etc/kubernetes/pki/apiserver-etcd-client.key --etcd-servers=https://127.0.0.1:2379 --kubelet-client-certificate=/etc/kubernetes/pki/apiserver-kubelet-client.crt --kubelet-client-key=/etc/kubernetes/pki/apiserver-kubelet-client.key --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname --proxy-client-cert-file=/etc/kubernetes/pki/front-proxy-client.crt --proxy-client-key-file=/etc/kubernetes/pki/front-proxy-client.key --requestheader-allowed-names=front-proxy-client --requestheader-client-ca-file=/etc/kubernetes/pki/front-proxy-ca.crt --requestheader-extra-headers-prefix=X-Remote-Extra- --requestheader-group-headers=X-Remote-Group --requestheader-username-headers=X-Remote-User --secure-port=6443 --service-account-issuer=https://kubernetes.default.svc.cluster.local --service-account-key-file=/etc/kubernetes/pki/sa.pub --service-account-signing-key-file=/etc/kubernetes/pki/sa.key --service-cluster-ip-range=10.96.0.0/12 --tls-cert-file=/etc/kubernetes/pki/apiserver.crt --tls-private-key-file=/etc/kubernetes/pki/apiserver.key
root       17031  0.0  0.0   3304   720 pts/0    S+   06:15   0:00 grep --color=auto etcd


controlplane $ strace -p 1976
strace: Process 1976 attached
futex(0x5a67d80, FUTEX_WAIT_PRIVATE, 0, NULL
^Cstrace: Process 1976 detached
 <detached ...>



strace -p 1976 -f

########List sysalls

controlplane $ strace -p 1976 -f -cw
strace: Process 1976 attached with 7 threads
strace: Process 17646 attached
^Cstrace: Process 1976 detached
strace: Process 2014 detached
strace: Process 2015 detached
strace: Process 2036 detached
strace: Process 2038 detached
strace: Process 2039 detached
strace: Process 2641 detached
strace: Process 17646 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 71.14   31.585065       15369      2055       878 futex
 24.10   10.698511        2799      3821           epoll_pwait
  4.13    1.833681         343      5344           nanosleep
  0.21    0.095022         225       421           write
  0.15    0.065463         307       213           sched_yield
  0.13    0.055902          57       975       474 read
  0.09    0.040799       40798         1         1 restart_syscall
  0.02    0.009510          88       107           rt_sigreturn
  0.01    0.002903          32        89           getrandom
  0.01    0.002598          24       107           tgkill
  0.00    0.002211         184        12           close
  0.00    0.002092          24        84           setsockopt
  0.00    0.002020          18       107           getpid
  0.00    0.001697        1697         1           clone
  0.00    0.001049          43        24        12 accept4
  0.00    0.000796          33        24           epoll_ctl
  0.00    0.000343          28        12           getsockname
  0.00    0.000082          27         3           rt_sigprocmask
  0.00    0.000053          26         2           sigaltstack
  0.00    0.000037          18         2           gettid
  0.00    0.000023          22         1           uname
------ ----------- ----------- --------- --------- ----------------
100.00   44.399857                 13405      1365 total




########Find open files

controlplane $ cd /proc/1976
controlplane $ ls
arch_status  cgroup      coredump_filter  exe      io         maps       mountstats  oom_adj        patch_state  sched      smaps         statm    timers
attr         clear_refs  cpuset           fd       limits     mem        net         oom_score      personality  schedstat  smaps_rollup  status   timerslack_ns
autogroup    cmdline     cwd              fdinfo   loginuid   mountinfo  ns          oom_score_adj  projid_map   sessionid  stack         syscall  uid_map
auxv         comm        environ          gid_map  map_files  mounts     numa_maps   pagemap        root         setgroups  stat          task     wchan
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ls -ltr exe 
lrwxrwxrwx 1 root root 0 Dec 17 06:01 exe -> /usr/local/bin/kube-apiserver
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd /proc/1921
controlplane $ 
controlplane $ 
controlplane $ ls -ltr exe 
lrwxrwxrwx 1 root root 0 Dec 17 06:01 exe -> /usr/local/bin/etcd
controlplane $ 
controlplane $ 
controlplane $ cd fd

 ### below are open files
controlplane $ ls -ltr
total 0
lrwx------ 1 root root 64 Dec 17 05:58 94 -> 'socket:[39522]'
lrwx------ 1 root root 64 Dec 17 05:58 93 -> 'socket:[39486]'
l-wx------ 1 root root 64 Dec 17 05:58 13 -> /var/lib/etcd/member/wal/0.tmp
lr-x------ 1 root root 64 Dec 17 05:58 12 -> /var/lib/etcd/member/wal
lrwx------ 1 root root 64 Dec 17 05:58 11 -> /var/lib/etcd/member/wal/0000000000000000-0000000000000000.wal
lrwx------ 1 root root 64 Dec 17 05:58 10 -> /var/lib/etcd/member/snap/db
l-wx------ 1 root root 64 Dec 17 05:58 1 -> 'pipe:[32129]'
lrwx------ 1 root root 64 Dec 17 05:58 0 -> /dev/null




##### Read Secret value from etcd

k create secret generic credit-card --from-literal cc=1234

tail 10


controlplane $ tail 10
6/registry/events/default/controlplane.180e8c71861e1650
*k8s


v1Event

controlplane.180e8c71861e1650default"*$c2bcc593-6c58-4d1a-a2bb-2f303739b0e32Ӈ˺
kubeletUpdatevԇ˺FieldsV1:
{"f:count":{},"f:firstTimestamp":{},"f:involvedObject":{},"f:lastTimestamp":{},"f:message":{},"f:reason":{},"f:reportingComponent":{},"f:reportingInstance":{},"f:source":{"f:component":{},"f:host":{}},"f:type":{}}B*
Node
    controlplane"
                 controlplane*2:NodeHasSufficientMemory"8Node controlplane status is now: NodeHasSufficientMemory*
kubelet
       controlplan͇͇˺JNormalRbrkubeletz
                                       controlplane"0Gcontrolplane $ 
controlplane $ 


controlplane $ cat 10 | grep 1234
Binary file (standard input) matches
controlplane $ 

controlplane $ 
controlplane $ 
controlplane $ cat 10 | strings | grep 1234
1234
controlplane $ 



controlplane $ cat 10 | strings | grep 1234 -A2 -B20
coordination.k8s.io/v1
Lease
kube-controller-manager
kube-system"
*$2b03e8d2-88b0-4f31-9a41-5f23741dcdda2
kube-controller-manager
Update
coordination.k8s.io/v1"
FieldsV1:|
z{"f:spec":{"f:acquireTime":{},"f:holderIdentity":{},"f:leaseDurationSeconds":{},"f:leaseTransitions":{},"f:renewTime":{}}}B
1controlplane_4b5079ee-7313-4ded-aa8c-d5ada57e71a7
%/registry/secrets/default/credit-card
Secret
credit-card
default"
*$7e3a9d34-5746-4a55-80b5-3570b45bd9b92
kubectl-create
Update
FieldsV1:+
){"f:data":{".":{},"f:cc":{}},"f:type":{}}B
1234
Opaque
+/registry/leases/kube-system/kube-scheduler
controlplane $ 

################################################################################################################################################
