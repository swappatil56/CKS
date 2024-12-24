# /proc access env variables

# Create apache pod with secret as environment variable
Read the secret from host filesystem

-- anyone can read secret if those who hav access to /proc directory on host



controlplane $ k run apache --image httpd --dry-run=client -oyaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: apache
  name: apache
spec:
  containers:
  - image: httpd
    name: apache
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
controlplane $ 
controlplane $ 
controlplane $ k run apache --image httpd --dry-run=client -oyaml > pod.yaml
bash: pod.yaml: No such file or directory
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k run apache --image httpd -o yaml --dry-run=client > pod.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/apache created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec apache -- env
PATH=/usr/local/apache2/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=apache
HTTPD_PREFIX=/usr/local/apache2
HTTPD_VERSION=2.4.62
HTTPD_SHA256=674188e7bf44ced82da8db522da946849e22080d73d16c93f7f4df89e25729ec
HTTPD_PATCHES=
SECRET=123456897556
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
KUBERNETES_SERVICE_HOST=10.96.0.1
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP_PROTO=tcp
HOME=/root
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ps aux | grep apache
root       28478  0.0  0.0   3304   724 pts/0    S+   06:40   0:00 grep --color=auto apache
controlplane $ ps aux | grep https 
root        1437  0.0  0.0   3896  1944 ?        SN   05:46   0:00 bash -c set -x; cd /opt; while ! curl -o theia-install.sh https://storage.googleapis.com/killercoda-prod-europe1/theia/theia-install.sh?v=82639; do sleep 1; done; bash theia-install.sh; rm theia-install.sh; nice -n 19 /opt/theia/node /opt/theia/browser-app/src-gen/backend/main.js /root --hostname=0.0.0.0 --port 40205
root        1921  1.8  3.1 11737972 64044 ?      Ssl  05:47   1:00 etcd --advertise-client-urls=https://172.30.1.2:2379 --cert-file=/etc/kubernetes/pki/etcd/server.crt --client-cert-auth=true --data-dir=/var/lib/etcd --experimental-initial-corrupt-check=true --experimental-watch-progress-notify-interval=5s --initial-advertise-peer-urls=https://172.30.1.2:2380 --initial-cluster=controlplane=https://172.30.1.2:2380 --key-file=/etc/kubernetes/pki/etcd/server.key --listen-client-urls=https://127.0.0.1:2379,https://172.30.1.2:2379 --listen-metrics-urls=http://127.0.0.1:2381 --listen-peer-urls=https://172.30.1.2:2380 --name=controlplane --peer-cert-file=/etc/kubernetes/pki/etcd/peer.crt --peer-client-cert-auth=true --peer-key-file=/etc/kubernetes/pki/etcd/peer.key --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt --snapshot-count=10000 --trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
root        1976  3.8 12.7 1519132 259400 ?      Ssl  05:47   2:01 kube-apiserver --advertise-address=172.30.1.2 --allow-privileged=true --authorization-mode=Node,RBAC --client-ca-file=/etc/kubernetes/pki/ca.crt --enable-admission-plugins=NodeRestriction --enable-bootstrap-token-auth=true --etcd-cafile=/etc/kubernetes/pki/etcd/ca.crt --etcd-certfile=/etc/kubernetes/pki/apiserver-etcd-client.crt --etcd-keyfile=/etc/kubernetes/pki/apiserver-etcd-client.key --etcd-servers=https://127.0.0.1:2379 --kubelet-client-certificate=/etc/kubernetes/pki/apiserver-kubelet-client.crt --kubelet-client-key=/etc/kubernetes/pki/apiserver-kubelet-client.key --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname --proxy-client-cert-file=/etc/kubernetes/pki/front-proxy-client.crt --proxy-client-key-file=/etc/kubernetes/pki/front-proxy-client.key --requestheader-allowed-names=front-proxy-client --requestheader-client-ca-file=/etc/kubernetes/pki/front-proxy-ca.crt --requestheader-extra-headers-prefix=X-Remote-Extra- --requestheader-group-headers=X-Remote-Group --requestheader-username-headers=X-Remote-User --secure-port=6443 --service-account-issuer=https://kubernetes.default.svc.cluster.local --service-account-key-file=/etc/kubernetes/pki/sa.pub --service-account-signing-key-file=/etc/kubernetes/pki/sa.key --service-cluster-ip-range=10.96.0.0/12 --tls-cert-file=/etc/kubernetes/pki/apiserver.crt --tls-private-key-file=/etc/kubernetes/pki/apiserver.key
root       28555  0.0  0.0   3304   720 pts/0    S+   06:40   0:00 grep --color=auto https
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ps aux | grep httpd
root       28563  0.0  0.0   3304   720 pts/0    S+   06:40   0:00 grep --color=auto httpd
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -o wide
NAME     READY   STATUS    RESTARTS   AGE    IP            NODE     NOMINATED NODE   READINESS GATES
apache   1/1     Running   0          101s   192.168.1.4   node01   <none>           <none>
controlplane $ 
controlplane $ 
controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
node01 $ 
node01 $ 
node01 $ ps aux | grep httpd
root       15215  0.0  0.2   5852  4700 ?        Ss   06:39   0:00 httpd -DFOREGROUND
www-data   15227  0.0  0.1 751792  3440 ?        Sl   06:39   0:00 httpd -DFOREGROUND
www-data   15228  0.0  0.1 751792  3440 ?        Sl   06:39   0:00 httpd -DFOREGROUND
www-data   15229  0.0  0.1 751792  3440 ?        Sl   06:39   0:00 httpd -DFOREGROUND
root       15763  0.0  0.0   3304   660 pts/0    S+   06:41   0:00 grep --color=auto httpd
node01 $ 
node01 $ 





pstree -p 

15215



node01 $ pstree -p
systemd(1)-+-ModemManager(611)-+-{ModemManager}(741)
           |                   `-{ModemManager}(747)
           |-accounts-daemon(546)-+-{accounts-daemon}(565)
           |                      `-{accounts-daemon}(595)
           |-agetty(655)
           |-agetty(658)
           |-atd(627)
           |-bash(2879)---kc-terminal(2881)
           |-containerd(625)-+-{containerd}(731)
           |                 |-{containerd}(733)
           |                 |-{containerd}(760)
           |                 |-{containerd}(761)
           |                 |-{containerd}(775)
           |                 |-{containerd}(804)
           |                 |-{containerd}(808)
           |                 |-{containerd}(1625)
           |                 |-{containerd}(1750)
           |                 |-{containerd}(2765)
           |                 `-{containerd}(2766)
           |-containerd-shim(1668)-+-flanneld(2173)-+-{flanneld}(2183)
           |                       |                |-{flanneld}(2184)
           |                       |                |-{flanneld}(2185)
           |                       |                |-{flanneld}(2186)
           |                       |                |-{flanneld}(2210)
           |                       |                `-{flanneld}(2212)
           |                       |-pause(1719)
           |                       |-runsvdir(2137)-+-runsv(2217)---calico-node(2222)-+-{calico-node}(2235)
           |                       |                |                                 |-{calico-node}(2236)
           |                       |                |                                 |-{calico-node}(2241)
           |                       |                |                                 |-{calico-node}(2254)
           |                       |                |                                 |-{calico-node}(2257)
           |                       |                |                                 |-{calico-node}(2261)
           |                       |                |                                 `-{calico-node}(2265)
           |                       |                |-runsv(2218)---calico-node(2226)-+-{calico-node}(2233)
           |                       |                |                                 |-{calico-node}(2234)
           |                       |                |                                 |-{calico-node}(2240)
           |                       |                |                                 |-{calico-node}(2260)
           |                       |                |                                 |-{calico-node}(2264)
           |                       |                |                                 |-{calico-node}(2266)
           |                       |                |                                 `-{calico-node}(2267)
           |                       |                |-runsv(2219)---calico-node(2225)-+-{calico-node}(2231)
           |                       |                |                                 |-{calico-node}(2232)
           |                       |                |                                 |-{calico-node}(2239)
           |                       |                |                                 |-{calico-node}(2248)
           |                       |                |                                 |-{calico-node}(2249)
           |                       |                |                                 |-{calico-node}(2250)
           |                       |                |                                 `-{calico-node}(2251)
           |                       |                |-runsv(2220)---calico-node(2223)-+-{calico-node}(2229)
           |                       |                |                                 |-{calico-node}(2230)
           |                       |                |                                 |-{calico-node}(2237)
           |                       |                |                                 |-{calico-node}(2253)
           |                       |                |                                 |-{calico-node}(2255)
           |                       |                |                                 |-{calico-node}(2259)
           |                       |                |                                 |-{calico-node}(2263)
           |                       |                |                                 |-{calico-node}(2337)
           |                       |                |                                 |-{calico-node}(2338)
           |                       |                |                                 |-{calico-node}(2390)
           |                       |                |                                 |-{calico-node}(2393)
           |                       |                |                                 `-{calico-node}(2394)
           |                       |                `-runsv(2221)---calico-node(2224)-+-{calico-node}(2227)
           |                       |                                                  |-{calico-node}(2228)
           |                       |                                                  |-{calico-node}(2238)
           |                       |                                                  |-{calico-node}(2252)
           |                       |                                                  |-{calico-node}(2256)
           |                       |                                                  |-{calico-node}(2258)
           |                       |                                                  `-{calico-node}(2262)
           |                       |-{containerd-shim}(1670)
           |                       |-{containerd-shim}(1671)
           |                       |-{containerd-shim}(1672)
           |                       |-{containerd-shim}(1676)
           |                       |-{containerd-shim}(1679)
           |                       |-{containerd-shim}(1680)
           |                       |-{containerd-shim}(1681)
           |                       |-{containerd-shim}(1682)
           |                       |-{containerd-shim}(1683)
           |                       |-{containerd-shim}(1735)
           |                       `-{containerd-shim}(1739)
           |-containerd-shim(1669)-+-kube-proxy(1776)-+-{kube-proxy}(1791)
           |                       |                  |-{kube-proxy}(1792)
           |                       |                  `-{kube-proxy}(1793)
           |                       |-pause(1725)
           |                       |-{containerd-shim}(1673)
           |                       |-{containerd-shim}(1674)
           |                       |-{containerd-shim}(1675)
           |                       |-{containerd-shim}(1677)
           |                       |-{containerd-shim}(1678)
           |                       |-{containerd-shim}(1684)
           |                       |-{containerd-shim}(1685)
           |                       |-{containerd-shim}(1686)
           |                       |-{containerd-shim}(1687)
           |                       |-{containerd-shim}(1731)
           |                       |-{containerd-shim}(1736)
           |                       `-{containerd-shim}(1737)
           |-containerd-shim(2686)-+-coredns(2793)-+-{coredns}(2821)
           |                       |               |-{coredns}(2822)
           |                       |               |-{coredns}(2823)
           |                       |               |-{coredns}(2840)
           |                       |               `-{coredns}(3476)
           |                       |-pause(2729)
           |                       |-{containerd-shim}(2688)
           |                       |-{containerd-shim}(2689)
           |                       |-{containerd-shim}(2690)
           |                       |-{containerd-shim}(2694)
           |                       |-{containerd-shim}(2695)
           |                       |-{containerd-shim}(2696)
           |                       |-{containerd-shim}(2697)
           |                       |-{containerd-shim}(2698)
           |                       |-{containerd-shim}(2699)
           |                       |-{containerd-shim}(2745)
           |                       `-{containerd-shim}(2747)
           |-containerd-shim(2687)-+-coredns(2825)-+-{coredns}(2838)
           |                       |               |-{coredns}(2839)
           |                       |               |-{coredns}(2841)
           |                       |               |-{coredns}(2842)
           |                       |               `-{coredns}(2843)
           |                       |-pause(2749)
           |                       |-{containerd-shim}(2691)
           |                       |-{containerd-shim}(2692)
           |                       |-{containerd-shim}(2693)
           |                       |-{containerd-shim}(2700)
           |                       |-{containerd-shim}(2701)
           |                       |-{containerd-shim}(2702)
           |                       |-{containerd-shim}(2703)
           |                       |-{containerd-shim}(2705)
           |                       |-{containerd-shim}(2706)
           |                       |-{containerd-shim}(2707)
           |                       |-{containerd-shim}(2708)
           |                       `-{containerd-shim}(2709)
           |-containerd-shim(15118)-+-httpd(15215)-+-httpd(15227)-+-{httpd}(15285)
           |                        |              |              |-{httpd}(15286)
           |                        |              |              |-{httpd}(15287)
           |                        |              |              |-{httpd}(15288)
           |                        |              |              |-{httpd}(15289)
           |                        |              |              |-{httpd}(15290)
           |                        |              |              |-{httpd}(15291)
           |                        |              |              |-{httpd}(15292)
           |                        |              |              |-{httpd}(15293)
           |                        |              |              |-{httpd}(15294)
           |                        |              |              |-{httpd}(15295)
           |                        |              |              |-{httpd}(15296)
           |                        |              |              |-{httpd}(15297)
           |                        |              |              |-{httpd}(15298)
           |                        |              |              |-{httpd}(15299)
           |                        |              |              |-{httpd}(15300)
           |                        |              |              |-{httpd}(15301)
           |                        |              |              |-{httpd}(15302)
           |                        |              |              |-{httpd}(15303)
           |                        |              |              |-{httpd}(15304)
           |                        |              |              |-{httpd}(15305)
           |                        |              |              |-{httpd}(15306)
           |                        |              |              |-{httpd}(15307)
           |                        |              |              |-{httpd}(15308)
           |                        |              |              |-{httpd}(15309)
           |                        |              |              `-{httpd}(15310)
           |                        |              |-httpd(15228)-+-{httpd}(15259)
           |                        |              |              |-{httpd}(15260)
           |                        |              |              |-{httpd}(15261)
           |                        |              |              |-{httpd}(15262)
           |                        |              |              |-{httpd}(15263)
           |                        |              |              |-{httpd}(15264)
           |                        |              |              |-{httpd}(15265)
           |                        |              |              |-{httpd}(15266)
           |                        |              |              |-{httpd}(15267)
           |                        |              |              |-{httpd}(15268)
           |                        |              |              |-{httpd}(15269)
           |                        |              |              |-{httpd}(15270)
           |                        |              |              |-{httpd}(15271)
           |                        |              |              |-{httpd}(15272)
           |                        |              |              |-{httpd}(15273)
           |                        |              |              |-{httpd}(15274)
           |                        |              |              |-{httpd}(15275)
           |                        |              |              |-{httpd}(15276)
           |                        |              |              |-{httpd}(15277)
           |                        |              |              |-{httpd}(15278)
           |                        |              |              |-{httpd}(15279)
           |                        |              |              |-{httpd}(15280)
           |                        |              |              |-{httpd}(15281)
           |                        |              |              |-{httpd}(15282)
           |                        |              |              |-{httpd}(15283)
           |                        |              |              `-{httpd}(15284)
           |                        |              `-httpd(15229)-+-{httpd}(15233)
           |                        |                             |-{httpd}(15234)
           |                        |                             |-{httpd}(15235)
           |                        |                             |-{httpd}(15236)
           |                        |                             |-{httpd}(15237)
           |                        |                             |-{httpd}(15238)
           |                        |                             |-{httpd}(15239)
           |                        |                             |-{httpd}(15240)
           |                        |                             |-{httpd}(15241)
           |                        |                             |-{httpd}(15242)
           |                        |                             |-{httpd}(15243)
           |                        |                             |-{httpd}(15244)
           |                        |                             |-{httpd}(15245)
           |                        |                             |-{httpd}(15246)
           |                        |                             |-{httpd}(15247)
           |                        |                             |-{httpd}(15248)
           |                        |                             |-{httpd}(15249)
           |                        |                             |-{httpd}(15250)
           |                        |                             |-{httpd}(15251)
           |                        |                             |-{httpd}(15252)
           |                        |                             |-{httpd}(15253)
           |                        |                             |-{httpd}(15254)
           |                        |                             |-{httpd}(15255)
           |                        |                             |-{httpd}(15256)
           |                        |                             |-{httpd}(15257)
           |                        |                             `-{httpd}(15258)
           |                        |-pause(15146)
           |                        |-{containerd-shim}(15119)
           |                        |-{containerd-shim}(15120)
           |                        |-{containerd-shim}(15121)
           |                        |-{containerd-shim}(15122)
           |                        |-{containerd-shim}(15123)
           |                        |-{containerd-shim}(15124)
           |                        |-{containerd-shim}(15125)
           |                        |-{containerd-shim}(15126)
           |                        |-{containerd-shim}(15127)
           |                        |-{containerd-shim}(15128)
           |                        `-{containerd-shim}(15157)
           |-cron(620)
           |-dbus-daemon(547)
           |-dhclient(681)-+-{dhclient}(682)
           |               |-{dhclient}(683)
           |               `-{dhclient}(684)
           |-dhclient(816)-+-{dhclient}(817)
           |               |-{dhclient}(818)
           |               `-{dhclient}(819)
           |-dhclient(845)-+-{dhclient}(846)
           |               |-{dhclient}(847)
           |               `-{dhclient}(848)
           |-dockerd(852)-+-{dockerd}(867)
           |              |-{dockerd}(868)
           |              |-{dockerd}(869)
           |              |-{dockerd}(888)
           |              |-{dockerd}(889)
           |              |-{dockerd}(890)
           |              `-{dockerd}(1054)
           |-kubelet(1410)-+-{kubelet}(1411)
           |               |-{kubelet}(1412)
           |               |-{kubelet}(1413)
           |               |-{kubelet}(1415)
           |               |-{kubelet}(1416)
           |               |-{kubelet}(1422)
           |               |-{kubelet}(1436)
           |               |-{kubelet}(1439)
           |               |-{kubelet}(1440)
           |               `-{kubelet}(1442)
           |-multipathd(476)-+-{multipathd}(477)
           |                 |-{multipathd}(478)
           |                 |-{multipathd}(479)
           |                 |-{multipathd}(480)
           |                 |-{multipathd}(481)
           |                 `-{multipathd}(482)
           |-networkd-dispat(553)
           |-polkitd(555)-+-{polkitd}(564)
           |              `-{polkitd}(596)
           |-rsyslogd(557)-+-{rsyslogd}(568)
           |               |-{rsyslogd}(569)
           |               `-{rsyslogd}(570)
           |-runtime-info-se(2854)-+-{runtime-info-se}(2856)
           |                       |-{runtime-info-se}(2857)
           |                       `-{runtime-info-se}(2858)
           |-snapd(1224)-+-{snapd}(1242)
           |             |-{snapd}(1243)
           |             |-{snapd}(1244)
           |             |-{snapd}(1245)
           |             |-{snapd}(1249)
           |             |-{snapd}(1250)
           |             |-{snapd}(1556)
           |             `-{snapd}(2007)
           |-sshd(675)---sshd(15712)---bash(15714)---pstree(16195)
           |-systemd-journal(352)
           |-systemd-logind(559)
           |-systemd-network(386)
           |-systemd-resolve(917)
           |-systemd-timesyn(887)---{systemd-timesyn}(896)
           |-systemd-udevd(382)
           |-udisksd(560)-+-{udisksd}(574)
           |              |-{udisksd}(598)
           |              |-{udisksd}(639)
           |              `-{udisksd}(748)
           `-unattended-upgr(764)---{unattended-upgr}(823)
node01 $ 



node01 $ cd /proc/15215
node01 $ ls
arch_status  cgroup      coredump_filter  exe      io         maps       mountstats  oom_adj        patch_state  sched      smaps         statm    timers
attr         clear_refs  cpuset           fd       limits     mem        net         oom_score      personality  schedstat  smaps_rollup  status   timerslack_ns
autogroup    cmdline     cwd              fdinfo   loginuid   mountinfo  ns          oom_score_adj  projid_map   sessionid  stack         syscall  uid_map
auxv         comm        environ          gid_map  map_files  mounts     numa_maps   pagemap        root         setgroups  stat          task     wchan
node01 $ 
node01 $ 
node01 $ 
node01 $ ls -ltr exe 
lrwxrwxrwx 1 root root 0 Dec 17 06:44 exe -> /usr/local/apache2/bin/httpd
node01 $ 
node01 $ 



# openfiles -  fd

node01 $ cd fd
node01 $ ls -ltr
total 0
l-wx------ 1 root root 64 Dec 17 06:42 7 -> 'pipe:[128936]'
l-wx------ 1 root root 64 Dec 17 06:42 6 -> 'pipe:[129062]'
lr-x------ 1 root root 64 Dec 17 06:42 5 -> 'pipe:[129062]'
lrwx------ 1 root root 64 Dec 17 06:42 4 -> 'socket:[129051]'
lrwx------ 1 root root 64 Dec 17 06:42 3 -> 'socket:[129050]'
l-wx------ 1 root root 64 Dec 17 06:42 2 -> 'pipe:[128937]'
l-wx------ 1 root root 64 Dec 17 06:42 1 -> 'pipe:[128936]'
lrwx------ 1 root root 64 Dec 17 06:42 0 -> /dev/null
node01 $ 


# environ file

node01 $ cd .. 
node01 $ ls -ltr
total 0
-r--r--r--  1 root root 0 Dec 17 06:42 limits
dr-x------  2 root root 0 Dec 17 06:42 fd
dr-xr-xr-x  3 root root 0 Dec 17 06:43 task
-r--r--r--  1 root root 0 Dec 17 06:43 stat
dr-x--x--x  2 root root 0 Dec 17 06:43 ns
-r--r--r--  1 root root 0 Dec 17 06:44 statm
lrwxrwxrwx  1 root root 0 Dec 17 06:44 exe -> /usr/local/apache2/bin/httpd
-r--------  1 root root 0 Dec 17 06:44 environ
-rw-r--r--  1 root root 0 Dec 17 06:44 comm
-r--r--r--  1 root root 0 Dec 17 06:44 cmdline
-r--r--r--  1 root root 0 Dec 17 06:44 wchan
-rw-r--r--  1 root root 0 Dec 17 06:44 uid_map
-rw-rw-rw-  1 root root 0 Dec 17 06:44 timerslack_ns
-r--r--r--  1 root root 0 Dec 17 06:44 timers
-r--------  1 root root 0 Dec 17 06:44 syscall
-r--r--r--  1 root root 0 Dec 17 06:44 status
-r--------  1 root root 0 Dec 17 06:44 stack
-r--r--r--  1 root root 0 Dec 17 06:44 smaps_rollup
-r--r--r--  1 root root 0 Dec 17 06:44 smaps
-rw-r--r--  1 root root 0 Dec 17 06:44 setgroups
-r--r--r--  1 root root 0 Dec 17 06:44 sessionid
-r--r--r--  1 root root 0 Dec 17 06:44 schedstat
-rw-r--r--  1 root root 0 Dec 17 06:44 sched
lrwxrwxrwx  1 root root 0 Dec 17 06:44 root -> /
-rw-r--r--  1 root root 0 Dec 17 06:44 projid_map
-r--------  1 root root 0 Dec 17 06:44 personality
-r--------  1 root root 0 Dec 17 06:44 patch_state
-r--------  1 root root 0 Dec 17 06:44 pagemap
-rw-r--r--  1 root root 0 Dec 17 06:44 oom_score_adj
-r--r--r--  1 root root 0 Dec 17 06:44 oom_score
-rw-r--r--  1 root root 0 Dec 17 06:44 oom_adj
-r--r--r--  1 root root 0 Dec 17 06:44 numa_maps
dr-xr-xr-x 56 root root 0 Dec 17 06:44 net
-r--------  1 root root 0 Dec 17 06:44 mountstats
-r--r--r--  1 root root 0 Dec 17 06:44 mounts
-r--r--r--  1 root root 0 Dec 17 06:44 mountinfo
-rw-------  1 root root 0 Dec 17 06:44 mem
-r--r--r--  1 root root 0 Dec 17 06:44 maps
dr-x------  2 root root 0 Dec 17 06:44 map_files
-rw-r--r--  1 root root 0 Dec 17 06:44 loginuid
-r--------  1 root root 0 Dec 17 06:44 io
-rw-r--r--  1 root root 0 Dec 17 06:44 gid_map
dr-x------  2 root root 0 Dec 17 06:44 fdinfo
lrwxrwxrwx  1 root root 0 Dec 17 06:44 cwd -> /usr/local/apache2
-r--r--r--  1 root root 0 Dec 17 06:44 cpuset
-rw-r--r--  1 root root 0 Dec 17 06:44 coredump_filter
--w-------  1 root root 0 Dec 17 06:44 clear_refs
-r--r--r--  1 root root 0 Dec 17 06:44 cgroup
-r--------  1 root root 0 Dec 17 06:44 auxv
-rw-r--r--  1 root root 0 Dec 17 06:44 autogroup
dr-xr-xr-x  2 root root 0 Dec 17 06:44 attr
-r--r--r--  1 root root 0 Dec 17 06:44 arch_status
node01 $ 
node01 $ 
node01 $ cat environ 
HTTPD_VERSION=2.4.62KUBERNETES_SERVICE_PORT=443KUBERNETES_PORT=tcp://10.96.0.1:443HOSTNAME=apacheHOME=/rootHTTPD_PATCHES=KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1PATH=/usr/local/apache2/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/binKUBERNETES_PORT_443_TCP_PORT=443HTTPD_SHA256=674188e7bf44ced82da8db522da946849e22080d73d16c93f7f4df89e25729ecKUBERNETES_PORT_443_TCP_PROTO=tcpSECRET=123456897556HTTPD_PREFIX=/usr/local/apache2KUBERNETES_SERVICE_PORT_HTTPS=443KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443KUBERNETES_SERVICE_HOST=10.96.0.1PWD=/usr/local/apache2node01 $ 
node01 $ 