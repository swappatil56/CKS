## create secret and Investigate the json audit log



controlplane $ cd /etc/kubernetes/audit/
controlplane $ vi policy.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
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
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
b438f304a4405       1766f54c897f0       15 seconds ago      Running             kube-scheduler            3                   eec624afbb541       kube-scheduler-controlplane
43f906730f21b       045733566833c       16 seconds ago      Running             kube-controller-manager   3                   8884fef65eb98       kube-controller-manager-controlplane
83e9faf15534a       95fef08b8bf89       36 minutes ago      Running             local-path-provisioner    2                   21ca97efc5e16       local-path-provisioner-6c5cff8948-phnkg
f109c304ba680       f9c3c1813269c       36 minutes ago      Running             calico-kube-controllers   2                   97f86f83c5726       calico-kube-controllers-94fb6bc47-wr56s
335cdeb6973f6       e6ea68648f0cd       36 minutes ago      Running             kube-flannel              1                   533265d0eda47       canal-cgrhr
05bd14b6ae927       75392e3500e36       36 minutes ago      Running             calico-node               1                   533265d0eda47       canal-cgrhr
985338ed7a9cb       ad83b2ca7b09e       37 minutes ago      Running             kube-proxy                2                   09808d4db9b4a       kube-proxy-bt2pv
fbd16cba46f7a       2e96e5913fc06       37 minutes ago      Running             etcd                      2                   02a53b18f1d9b       etcd-controlplane
01f248fb9d991       604f5db92eaa8       37 minutes ago      Running             kube-apiserver            2                   1e6e89452591c       kube-apiserver-controlplane
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
b438f304a4405       1766f54c897f0       22 seconds ago      Running             kube-scheduler            3                   eec624afbb541       kube-scheduler-controlplane
43f906730f21b       045733566833c       23 seconds ago      Running             kube-controller-manager   3                   8884fef65eb98       kube-controller-manager-controlplane
83e9faf15534a       95fef08b8bf89       36 minutes ago      Running             local-path-provisioner    2                   21ca97efc5e16       local-path-provisioner-6c5cff8948-phnkg
f109c304ba680       f9c3c1813269c       36 minutes ago      Running             calico-kube-controllers   2                   97f86f83c5726       calico-kube-controllers-94fb6bc47-wr56s
335cdeb6973f6       e6ea68648f0cd       36 minutes ago      Running             kube-flannel              1                   533265d0eda47       canal-cgrhr
05bd14b6ae927       75392e3500e36       36 minutes ago      Running             calico-node               1                   533265d0eda47       canal-cgrhr
985338ed7a9cb       ad83b2ca7b09e       37 minutes ago      Running             kube-proxy                2                   09808d4db9b4a       kube-proxy-bt2pv
fbd16cba46f7a       2e96e5913fc06       37 minutes ago      Running             etcd                      2                   02a53b18f1d9b       etcd-controlplane
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
b438f304a4405       1766f54c897f0       26 seconds ago      Running             kube-scheduler            3                   eec624afbb541       kube-scheduler-controlplane
43f906730f21b       045733566833c       27 seconds ago      Running             kube-controller-manager   3                   8884fef65eb98       kube-controller-manager-controlplane
83e9faf15534a       95fef08b8bf89       36 minutes ago      Running             local-path-provisioner    2                   21ca97efc5e16       local-path-provisioner-6c5cff8948-phnkg
f109c304ba680       f9c3c1813269c       36 minutes ago      Running             calico-kube-controllers   2                   97f86f83c5726       calico-kube-controllers-94fb6bc47-wr56s
335cdeb6973f6       e6ea68648f0cd       36 minutes ago      Running             kube-flannel              1                   533265d0eda47       canal-cgrhr
05bd14b6ae927       75392e3500e36       37 minutes ago      Running             calico-node               1                   533265d0eda47       canal-cgrhr
985338ed7a9cb       ad83b2ca7b09e       37 minutes ago      Running             kube-proxy                2                   09808d4db9b4a       kube-proxy-bt2pv
fbd16cba46f7a       2e96e5913fc06       37 minutes ago      Running             etcd                      2                   02a53b18f1d9b       etcd-controlplane
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
Get "https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods?limit=500": dial tcp 172.30.1.2:6443: connect: connection refused - error from a previous attempt: read tcp 172.30.1.2:42358->172.30.1.2:6443: read: connection reset by peer
controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
The connection to the server 172.30.1.2:6443 was refused - did you specify the right host or port?
controlplane $ k get pod -n kube-system
Error from server (Forbidden): pods is forbidden: User "kubernetes-admin" cannot list resource "pods" in API group "" in the namespace "kube-system"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   0/1     Running   3 (30s ago)   11d
canal-cgrhr                               2/2     Running   2 (38m ago)   11d
canal-jb5rr                               2/2     Running   2 (38m ago)   11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (38m ago)   11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (38m ago)   11d
etcd-controlplane                         1/1     Running   2 (38m ago)   11d
kube-apiserver-controlplane               0/1     Pending   0             5s
kube-controller-manager-controlplane      1/1     Running   3 (76s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (38m ago)   11d
kube-proxy-bt2pv                          1/1     Running   2 (38m ago)   11d
kube-scheduler-controlplane               1/1     Running   3 (76s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-94fb6bc47-wr56s   0/1     Running   3 (33s ago)   11d
canal-cgrhr                               2/2     Running   2 (38m ago)   11d
canal-jb5rr                               2/2     Running   2 (38m ago)   11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (38m ago)   11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (38m ago)   11d
etcd-controlplane                         1/1     Running   2 (38m ago)   11d
kube-apiserver-controlplane               0/1     Pending   0             8s
kube-controller-manager-controlplane      1/1     Running   3 (79s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (38m ago)   11d
kube-proxy-bt2pv                          1/1     Running   2 (38m ago)   11d
kube-scheduler-controlplane               1/1     Running   3 (79s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k delete pod kube-apiserver-controlplane -n kube-system
pod "kube-apiserver-controlplane" deleted




^Ccontrolplane $ k delete pod kube-apiserver-controlplane -n kube-system --force
Warning: Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.
pod "kube-apiserver-controlplane" force deleted
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS       AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   3 (57s ago)    11d
canal-cgrhr                               2/2     Running   2 (39m ago)    11d
canal-jb5rr                               2/2     Running   2 (39m ago)    11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (39m ago)    11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (39m ago)    11d
etcd-controlplane                         1/1     Running   2 (39m ago)    11d
kube-controller-manager-controlplane      1/1     Running   3 (103s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (39m ago)    11d
kube-proxy-bt2pv                          1/1     Running   2 (39m ago)    11d
kube-scheduler-controlplane               1/1     Running   3 (103s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS       AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   3 (63s ago)    11d
canal-cgrhr                               2/2     Running   2 (39m ago)    11d
canal-jb5rr                               2/2     Running   2 (39m ago)    11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (39m ago)    11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (39m ago)    11d
etcd-controlplane                         1/1     Running   2 (39m ago)    11d
kube-controller-manager-controlplane      1/1     Running   3 (109s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (39m ago)    11d
kube-proxy-bt2pv                          1/1     Running   2 (39m ago)    11d
kube-scheduler-controlplane               1/1     Running   3 (109s ago)   11d
controlplane $ k get pod -n kube-system | grep api
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system | grep api
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS       AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   3 (73s ago)    11d
canal-cgrhr                               2/2     Running   2 (39m ago)    11d
canal-jb5rr                               2/2     Running   2 (39m ago)    11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (39m ago)    11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (39m ago)    11d
etcd-controlplane                         1/1     Running   2 (39m ago)    11d
kube-controller-manager-controlplane      1/1     Running   3 (119s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (39m ago)    11d
kube-proxy-bt2pv                          1/1     Running   2 (39m ago)    11d
kube-scheduler-controlplane               1/1     Running   3 (119s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ crictl ps
CONTAINER           IMAGE               CREATED              STATE               NAME                      ATTEMPT             POD ID              POD
fedaabf96e373       604f5db92eaa8       55 seconds ago       Running             kube-apiserver            0                   f2b726276875c       kube-apiserver-controlplane
0b655a7b1a5ec       f9c3c1813269c       About a minute ago   Running             calico-kube-controllers   3                   97f86f83c5726       calico-kube-controllers-94fb6bc47-wr56s
b438f304a4405       1766f54c897f0       2 minutes ago        Running             kube-scheduler            3                   eec624afbb541       kube-scheduler-controlplane
43f906730f21b       045733566833c       2 minutes ago        Running             kube-controller-manager   3                   8884fef65eb98       kube-controller-manager-controlplane
83e9faf15534a       95fef08b8bf89       38 minutes ago       Running             local-path-provisioner    2                   21ca97efc5e16       local-path-provisioner-6c5cff8948-phnkg
335cdeb6973f6       e6ea68648f0cd       38 minutes ago       Running             kube-flannel              1                   533265d0eda47       canal-cgrhr
05bd14b6ae927       75392e3500e36       38 minutes ago       Running             calico-node               1                   533265d0eda47       canal-cgrhr
985338ed7a9cb       ad83b2ca7b09e       38 minutes ago       Running             kube-proxy                2                   09808d4db9b4a       kube-proxy-bt2pv
fbd16cba46f7a       2e96e5913fc06       39 minutes ago       Running             etcd                      2                   02a53b18f1d9b       etcd-controlplane
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS       AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   3 (80s ago)    11d
canal-cgrhr                               2/2     Running   2 (39m ago)    11d
canal-jb5rr                               2/2     Running   2 (39m ago)    11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (39m ago)    11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (39m ago)    11d
etcd-controlplane                         1/1     Running   2 (39m ago)    11d
kube-controller-manager-controlplane      1/1     Running   3 (2m6s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (39m ago)    11d
kube-proxy-bt2pv                          1/1     Running   2 (39m ago)    11d
kube-scheduler-controlplane               1/1     Running   3 (2m6s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS        AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   3 (86s ago)     11d
canal-cgrhr                               2/2     Running   2 (39m ago)     11d
canal-jb5rr                               2/2     Running   2 (39m ago)     11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (39m ago)     11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (39m ago)     11d
etcd-controlplane                         1/1     Running   2 (39m ago)     11d
kube-controller-manager-controlplane      1/1     Running   3 (2m12s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (39m ago)     11d
kube-proxy-bt2pv                          1/1     Running   2 (39m ago)     11d
kube-scheduler-controlplane               1/1     Running   3 (2m12s ago)   11d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k create secret generic very-secure --from-literal user=admin
secret/very-secure created
controlplane $ cd /etc/kubernetes/audit/ 
controlplane $ ls
audit.log  policy.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ tail -f audit.log 
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"a5c8369c-6583-408b-aa2a-777cc70a6319","stage":"RequestReceived","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","requestReceivedTimestamp":"2024-12-18T05:29:37.525583Z","stageTimestamp":"2024-12-18T05:29:37.525583Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"a5c8369c-6583-408b-aa2a-777cc70a6319","stage":"ResponseComplete","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:37.525583Z","stageTimestamp":"2024-12-18T05:29:37.526180Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:public-info-viewer\" of ClusterRole \"system:public-info-viewer\" to Group \"system:unauthenticated\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"3e6adfb4-7b36-4592-93c7-358f3b6fc27c","stage":"RequestReceived","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-controller-manager?timeout=5s","verb":"update","user":{"username":"system:kube-controller-manager","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-controller-manager/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-controller-manager","apiGroup":"coordination.k8s.io","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:29:37.981963Z","stageTimestamp":"2024-12-18T05:29:37.981963Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"3e6adfb4-7b36-4592-93c7-358f3b6fc27c","stage":"ResponseComplete","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-controller-manager?timeout=5s","verb":"update","user":{"username":"system:kube-controller-manager","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-controller-manager/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-controller-manager","uid":"2b03e8d2-88b0-4f31-9a41-5f23741dcdda","apiGroup":"coordination.k8s.io","apiVersion":"v1","resourceVersion":"5295"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:37.981963Z","stageTimestamp":"2024-12-18T05:29:37.986282Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:kube-controller-manager\" of ClusterRole \"system:kube-controller-manager\" to User \"system:kube-controller-manager\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"9e752294-7261-46ac-9d3d-d29877d92e89","stage":"RequestReceived","requestURI":"/apis/crd.projectcalico.org/v1/clusterinformations/default","verb":"get","user":{"username":"system:serviceaccount:kube-system:calico-kube-controllers","uid":"322d5a13-0a62-4bf3-8f9e-3a2bc16db559","groups":["system:serviceaccounts","system:serviceaccounts:kube-system","system:authenticated"],"extra":{"authentication.kubernetes.io/credential-id":["JTI=89466cbc-3e17-4ea0-9319-bf8c162d3065"],"authentication.kubernetes.io/node-name":["controlplane"],"authentication.kubernetes.io/node-uid":["59d11f1d-d27c-4268-ac5d-9ed42d283cc7"],"authentication.kubernetes.io/pod-name":["calico-kube-controllers-94fb6bc47-wr56s"],"authentication.kubernetes.io/pod-uid":["33dc4a2d-9449-4b80-ae4e-09237c0e3188"]}},"sourceIPs":["192.168.0.2"],"userAgent":"Go-http-client/2.0","objectRef":{"resource":"clusterinformations","name":"default","apiGroup":"crd.projectcalico.org","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:29:38.034202Z","stageTimestamp":"2024-12-18T05:29:38.034202Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"9e752294-7261-46ac-9d3d-d29877d92e89","stage":"ResponseComplete","requestURI":"/apis/crd.projectcalico.org/v1/clusterinformations/default","verb":"get","user":{"username":"system:serviceaccount:kube-system:calico-kube-controllers","uid":"322d5a13-0a62-4bf3-8f9e-3a2bc16db559","groups":["system:serviceaccounts","system:serviceaccounts:kube-system","system:authenticated"],"extra":{"authentication.kubernetes.io/credential-id":["JTI=89466cbc-3e17-4ea0-9319-bf8c162d3065"],"authentication.kubernetes.io/node-name":["controlplane"],"authentication.kubernetes.io/node-uid":["59d11f1d-d27c-4268-ac5d-9ed42d283cc7"],"authentication.kubernetes.io/pod-name":["calico-kube-controllers-94fb6bc47-wr56s"],"authentication.kubernetes.io/pod-uid":["33dc4a2d-9449-4b80-ae4e-09237c0e3188"]}},"sourceIPs":["192.168.0.2"],"userAgent":"Go-http-client/2.0","objectRef":{"resource":"clusterinformations","name":"default","apiGroup":"crd.projectcalico.org","apiVersion":"v1"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:38.034202Z","stageTimestamp":"2024-12-18T05:29:38.036980Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"calico-kube-controllers\" of ClusterRole \"calico-kube-controllers\" to ServiceAccount \"calico-kube-controllers/kube-system\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"9ecfcaf7-901c-44ee-ba77-4cb8e1f2f53e","stage":"RequestReceived","requestURI":"/healthz?timeout=20s","verb":"get","user":{"username":"system:serviceaccount:kube-system:calico-kube-controllers","uid":"322d5a13-0a62-4bf3-8f9e-3a2bc16db559","groups":["system:serviceaccounts","system:serviceaccounts:kube-system","system:authenticated"],"extra":{"authentication.kubernetes.io/credential-id":["JTI=89466cbc-3e17-4ea0-9319-bf8c162d3065"],"authentication.kubernetes.io/node-name":["controlplane"],"authentication.kubernetes.io/node-uid":["59d11f1d-d27c-4268-ac5d-9ed42d283cc7"],"authentication.kubernetes.io/pod-name":["calico-kube-controllers-94fb6bc47-wr56s"],"authentication.kubernetes.io/pod-uid":["33dc4a2d-9449-4b80-ae4e-09237c0e3188"]}},"sourceIPs":["192.168.0.2"],"userAgent":"kube-controllers/v0.0.0 (linux/amd64) kubernetes/$Format","requestReceivedTimestamp":"2024-12-18T05:29:38.047842Z","stageTimestamp":"2024-12-18T05:29:38.047842Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"9ecfcaf7-901c-44ee-ba77-4cb8e1f2f53e","stage":"ResponseComplete","requestURI":"/healthz?timeout=20s","verb":"get","user":{"username":"system:serviceaccount:kube-system:calico-kube-controllers","uid":"322d5a13-0a62-4bf3-8f9e-3a2bc16db559","groups":["system:serviceaccounts","system:serviceaccounts:kube-system","system:authenticated"],"extra":{"authentication.kubernetes.io/credential-id":["JTI=89466cbc-3e17-4ea0-9319-bf8c162d3065"],"authentication.kubernetes.io/node-name":["controlplane"],"authentication.kubernetes.io/node-uid":["59d11f1d-d27c-4268-ac5d-9ed42d283cc7"],"authentication.kubernetes.io/pod-name":["calico-kube-controllers-94fb6bc47-wr56s"],"authentication.kubernetes.io/pod-uid":["33dc4a2d-9449-4b80-ae4e-09237c0e3188"]}},"sourceIPs":["192.168.0.2"],"userAgent":"kube-controllers/v0.0.0 (linux/amd64) kubernetes/$Format","responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:38.047842Z","stageTimestamp":"2024-12-18T05:29:38.049772Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:public-info-viewer\" of ClusterRole \"system:public-info-viewer\" to Group \"system:authenticated\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"b0c03170-c21b-45f5-b3fc-a104ed6b0c97","stage":"RequestReceived","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-scheduler?timeout=5s","verb":"update","user":{"username":"system:kube-scheduler","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-scheduler/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-scheduler","apiGroup":"coordination.k8s.io","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:29:38.056063Z","stageTimestamp":"2024-12-18T05:29:38.056063Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"b0c03170-c21b-45f5-b3fc-a104ed6b0c97","stage":"ResponseComplete","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-scheduler?timeout=5s","verb":"update","user":{"username":"system:kube-scheduler","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-scheduler/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-scheduler","uid":"987ef19b-20af-4b07-9f09-8cd44e163fce","apiGroup":"coordination.k8s.io","apiVersion":"v1","resourceVersion":"5296"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:38.056063Z","stageTimestamp":"2024-12-18T05:29:38.060376Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:kube-scheduler\" of ClusterRole \"system:kube-scheduler\" to User \"system:kube-scheduler\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"eb24650b-07bc-4581-99e7-97ec93b37fea","stage":"RequestReceived","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","requestReceivedTimestamp":"2024-12-18T05:29:38.525321Z","stageTimestamp":"2024-12-18T05:29:38.525321Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"eb24650b-07bc-4581-99e7-97ec93b37fea","stage":"ResponseComplete","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:38.525321Z","stageTimestamp":"2024-12-18T05:29:38.527651Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:public-info-viewer\" of ClusterRole \"system:public-info-viewer\" to Group \"system:unauthenticated\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"531bd168-aae4-44a9-b516-019d8ccfdb45","stage":"RequestReceived","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","requestReceivedTimestamp":"2024-12-18T05:29:39.524877Z","stageTimestamp":"2024-12-18T05:29:39.524877Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"531bd168-aae4-44a9-b516-019d8ccfdb45","stage":"ResponseComplete","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:39.524877Z","stageTimestamp":"2024-12-18T05:29:39.528321Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:public-info-viewer\" of ClusterRole \"system:public-info-viewer\" to Group \"system:unauthenticated\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"fcc86d49-4370-45f1-9f92-d64783c70434","stage":"RequestReceived","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-controller-manager?timeout=5s","verb":"update","user":{"username":"system:kube-controller-manager","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-controller-manager/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-controller-manager","apiGroup":"coordination.k8s.io","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:29:39.988286Z","stageTimestamp":"2024-12-18T05:29:39.988286Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"fcc86d49-4370-45f1-9f92-d64783c70434","stage":"ResponseComplete","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-controller-manager?timeout=5s","verb":"update","user":{"username":"system:kube-controller-manager","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-controller-manager/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-controller-manager","uid":"2b03e8d2-88b0-4f31-9a41-5f23741dcdda","apiGroup":"coordination.k8s.io","apiVersion":"v1","resourceVersion":"5298"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:39.988286Z","stageTimestamp":"2024-12-18T05:29:39.992524Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:kube-controller-manager\" of ClusterRole \"system:kube-controller-manager\" to User \"system:kube-controller-manager\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"90ae0839-b992-419a-82f1-f2df37dd5a22","stage":"RequestReceived","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-scheduler?timeout=5s","verb":"update","user":{"username":"system:kube-scheduler","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-scheduler/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-scheduler","apiGroup":"coordination.k8s.io","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:29:40.061773Z","stageTimestamp":"2024-12-18T05:29:40.061773Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"90ae0839-b992-419a-82f1-f2df37dd5a22","stage":"ResponseComplete","requestURI":"/apis/coordination.k8s.io/v1/namespaces/kube-system/leases/kube-scheduler?timeout=5s","verb":"update","user":{"username":"system:kube-scheduler","groups":["system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-scheduler/v1.31.0 (linux/amd64) kubernetes/9edcffc/leader-election","objectRef":{"resource":"leases","namespace":"kube-system","name":"kube-scheduler","uid":"987ef19b-20af-4b07-9f09-8cd44e163fce","apiGroup":"coordination.k8s.io","apiVersion":"v1","resourceVersion":"5299"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:40.061773Z","stageTimestamp":"2024-12-18T05:29:40.067286Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:kube-scheduler\" of ClusterRole \"system:kube-scheduler\" to User \"system:kube-scheduler\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"6193fb9f-3320-4699-88ea-bd6bf8998164","stage":"RequestReceived","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","requestReceivedTimestamp":"2024-12-18T05:29:40.523434Z","stageTimestamp":"2024-12-18T05:29:40.523434Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"6193fb9f-3320-4699-88ea-bd6bf8998164","stage":"ResponseComplete","requestURI":"/readyz","verb":"get","user":{"username":"system:anonymous","groups":["system:unauthenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kube-probe/1.31","responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:29:40.523434Z","stageTimestamp":"2024-12-18T05:29:40.524613Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"system:public-info-viewer\" of ClusterRole \"system:public-info-viewer\" to Group \"system:unauthenticated\""}}
^C
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
NAME                                      READY   STATUS    RESTARTS        AGE
calico-kube-controllers-94fb6bc47-wr56s   1/1     Running   3 (2m24s ago)   11d
canal-cgrhr                               2/2     Running   2 (40m ago)     11d
canal-jb5rr                               2/2     Running   2 (40m ago)     11d
coredns-57888bfdc7-895dj                  1/1     Running   1 (40m ago)     11d
coredns-57888bfdc7-9rjt5                  1/1     Running   1 (40m ago)     11d
etcd-controlplane                         1/1     Running   2 (40m ago)     11d
kube-apiserver-controlplane               1/1     Running   0               43s
kube-controller-manager-controlplane      1/1     Running   3 (3m10s ago)   11d
kube-proxy-5xtp7                          1/1     Running   1 (40m ago)     11d
kube-proxy-bt2pv                          1/1     Running   2 (40m ago)     11d
kube-scheduler-controlplane               1/1     Running   3 (3m10s ago)   11d
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
controlplane $ cat audit.log  | grep 'very-secure'
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"22be49e7-e944-443d-9c79-ba27b9c78a33","stage":"ResponseComplete","requestURI":"/api/v1/namespaces/default/secrets?fieldManager=kubectl-create\u0026fieldValidation=Strict","verb":"create","user":{"username":"kubernetes-admin","groups":["kubeadm:cluster-admins","system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kubectl/v1.31.0 (linux/amd64) kubernetes/9edcffc","objectRef":{"resource":"secrets","namespace":"default","name":"very-secure","apiVersion":"v1"},"responseStatus":{"metadata":{},"code":201},"requestReceivedTimestamp":"2024-12-18T05:29:17.272555Z","stageTimestamp":"2024-12-18T05:29:17.279533Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"kubeadm:cluster-admins\" of ClusterRole \"cluster-admin\" to Group \"kubeadm:cluster-admins\""}}
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k edit secret very-secure
secret/very-secure edited
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat audit.log  | grep 'very-secure'
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"22be49e7-e944-443d-9c79-ba27b9c78a33","stage":"ResponseComplete","requestURI":"/api/v1/namespaces/default/secrets?fieldManager=kubectl-create\u0026fieldValidation=Strict","verb":"create","user":{"username":"kubernetes-admin","groups":["kubeadm:cluster-admins","system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kubectl/v1.31.0 (linux/amd64) kubernetes/9edcffc","objectRef":{"resource":"secrets","namespace":"default","name":"very-secure","apiVersion":"v1"},"responseStatus":{"metadata":{},"code":201},"requestReceivedTimestamp":"2024-12-18T05:29:17.272555Z","stageTimestamp":"2024-12-18T05:29:17.279533Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"kubeadm:cluster-admins\" of ClusterRole \"cluster-admin\" to Group \"kubeadm:cluster-admins\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"78c3e91f-9278-46ee-93b8-2c6486080b13","stage":"RequestReceived","requestURI":"/api/v1/namespaces/default/secrets/very-secure","verb":"get","user":{"username":"kubernetes-admin","groups":["kubeadm:cluster-admins","system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kubectl/v1.31.0 (linux/amd64) kubernetes/9edcffc","objectRef":{"resource":"secrets","namespace":"default","name":"very-secure","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:33:18.891118Z","stageTimestamp":"2024-12-18T05:33:18.891118Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"78c3e91f-9278-46ee-93b8-2c6486080b13","stage":"ResponseComplete","requestURI":"/api/v1/namespaces/default/secrets/very-secure","verb":"get","user":{"username":"kubernetes-admin","groups":["kubeadm:cluster-admins","system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kubectl/v1.31.0 (linux/amd64) kubernetes/9edcffc","objectRef":{"resource":"secrets","namespace":"default","name":"very-secure","apiVersion":"v1"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:33:18.891118Z","stageTimestamp":"2024-12-18T05:33:18.893955Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"kubeadm:cluster-admins\" of ClusterRole \"cluster-admin\" to Group \"kubeadm:cluster-admins\""}}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"5cbd26ec-54ec-4467-93be-540d85539aff","stage":"RequestReceived","requestURI":"/api/v1/namespaces/default/secrets/very-secure?fieldManager=kubectl-edit\u0026fieldValidation=Strict","verb":"patch","user":{"username":"kubernetes-admin","groups":["kubeadm:cluster-admins","system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kubectl/v1.31.0 (linux/amd64) kubernetes/9edcffc","objectRef":{"resource":"secrets","namespace":"default","name":"very-secure","apiVersion":"v1"},"requestReceivedTimestamp":"2024-12-18T05:33:38.036697Z","stageTimestamp":"2024-12-18T05:33:38.036697Z"}
{"kind":"Event","apiVersion":"audit.k8s.io/v1","level":"Metadata","auditID":"5cbd26ec-54ec-4467-93be-540d85539aff","stage":"ResponseComplete","requestURI":"/api/v1/namespaces/default/secrets/very-secure?fieldManager=kubectl-edit\u0026fieldValidation=Strict","verb":"patch","user":{"username":"kubernetes-admin","groups":["kubeadm:cluster-admins","system:authenticated"]},"sourceIPs":["172.30.1.2"],"userAgent":"kubectl/v1.31.0 (linux/amd64) kubernetes/9edcffc","objectRef":{"resource":"secrets","namespace":"default","name":"very-secure","apiVersion":"v1"},"responseStatus":{"metadata":{},"code":200},"requestReceivedTimestamp":"2024-12-18T05:33:38.036697Z","stageTimestamp":"2024-12-18T05:33:38.043081Z","annotations":{"authorization.k8s.io/decision":"allow","authorization.k8s.io/reason":"RBAC: allowed by ClusterRoleBinding \"kubeadm:cluster-admins\" of ClusterRole \"cluster-admin\" to Group \"kubeadm:cluster-admins\""}}
controlplane $ 
controlplane $ 