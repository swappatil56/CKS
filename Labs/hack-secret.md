Use context: kubectl config use-context restricted@infra-prod

You're asked to investigate a possible permission escape in Namespace restricted. The context authenticates as user restricted which has only limited permissions and shouldn't be able to read Secret values.

Try to find the password-key values of the Secrets secret1, secret2 and secret3 in Namespace restricted. Write the decoded plaintext values into files /opt/course/12/secret1, /opt/course/12/secret2 and /opt/course/12/secret3.


/ # curl https://kubernetes.default/api/v1/namespaces/restricted/secrets -H "Authorization: Bearer $(cat /run/secrets/kubernetes.io/serviceaccount/token)" -k
...
    {
      "metadata": {
        "name": "secret3",
        "namespace": "restricted",
...
          }
        ]
      },
      "data": {
        "password": "cEVuRXRSYVRpT24tdEVzVGVSCg=="
      },
      "type": "Opaque"
    }



controlplane $ k create ns
error: exactly one NAME is required, got 0
See 'kubectl create namespace -h' for help and examples
controlplane $ k create ns restricted
namespace/restricted created
controlplane $ 
controlplane $ 
controlplane $ k create secret secret1 -n restricted
error: unknown command "secret1"
See 'kubectl create secret -h' for help and examples
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k create secret generic secret1 --from-literal admin:swwap -n restricted
error: invalid literal source admin:swwap, expected key=value
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k create secret generic secret1 --from-literal admin=swap -n restricted
secret/secret1 created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k create secret generic secret2 --from-literal password=pass1234 -n restricted
secret/secret2 created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k create secret generic secret3 --from-literal new=secret -n restricted
secret/secret3 created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get secret -n restricted
NAME      TYPE     DATA   AGE
secret1   Opaque   1      75s
secret2   Opaque   1      39s
secret3   Opaque   1      10s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k run pod --image nginx --dry-run=client -o yaml > pod.yaml
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
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
pod/pod created
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME   READY   STATUS              RESTARTS   AGE
pod    0/1     ContainerCreating   0          3s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME   READY   STATUS              RESTARTS   AGE
pod    0/1     ContainerCreating   0          5s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME   READY   STATUS              RESTARTS   AGE
pod    0/1     ContainerCreating   0          8s
controlplane $ k get pod
NAME   READY   STATUS              RESTARTS   AGE
pod    0/1     ContainerCreating   0          12s
controlplane $ k delete pod pod --force
Warning: Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.
pod "pod" force deleted
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/pod created
controlplane $ 
controlplane $ k get pod
No resources found in default namespace.
controlplane $ k get pod -n restricted
NAME   READY   STATUS              RESTARTS   AGE
pod    0/1     ContainerCreating   0          7s
controlplane $ 
controlplane $ 
controlplane $ k get pod -n restricted
NAME   READY   STATUS              RESTARTS   AGE
pod    0/1     ContainerCreating   0          9s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k describe pod -n restricted
Name:             pod
Namespace:        restricted
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Sat, 21 Dec 2024 08:48:04 +0000
Labels:           run=pod
Annotations:      cni.projectcalico.org/containerID: 543b23b1cf9fdbdc79008b2dbfcf956ceabb10c648ffcffa0d69d58926d13132
                  cni.projectcalico.org/podIP: 192.168.1.4/32
                  cni.projectcalico.org/podIPs: 192.168.1.4/32
Status:           Running
IP:               192.168.1.4
IPs:
  IP:  192.168.1.4
Containers:
  pod:
    Container ID:   containerd://b5e22deac4f06510bc63611c1e45e256de41e3407e25d4e2211a632e5e796e88
    Image:          nginx
    Image ID:       docker.io/library/nginx@sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 21 Dec 2024 08:48:13 +0000
    Ready:          True
    Restart Count:  0
    Environment:
      secret1:  <set to the key 'admin' in secret 'secret1'>  Optional: false
    Mounts:
      /etc/secret2 from secret2 (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-c7vd7 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  secret2:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  secret2
    Optional:    false
  kube-api-access-c7vd7:
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
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  20s   default-scheduler  Successfully assigned restricted/pod to node01
  Normal  Pulling    19s   kubelet            Pulling image "nginx"
  Normal  Pulled     11s   kubelet            Successfully pulled image "nginx" in 8.124s (8.124s including waiting). Image size: 72099501 bytes.
  Normal  Created    11s   kubelet            Created container pod
  Normal  Started    11s   kubelet            Started container pod
controlplane $ k get pod -n restricted
NAME   READY   STATUS    RESTARTS   AGE
pod    1/1     Running   0          34s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n restricted
NAME   READY   STATUS    RESTARTS   AGE
pod    1/1     Running   0          3m49s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod pod -n restricted -o yaml | grep ^C
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec pod pod -n restricted -- env | grep secret
secret1=swap
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec pod pod -n restricted -- env | grep secret1
secret1=swap
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec pod pod -n restricted -- mount 
overlay on / type overlay (rw,relatime,lowerdir=/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/70/fs:/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/69/fs:/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/68/fs:/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/67/fs:/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/66/fs:/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/65/fs:/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/64/fs,upperdir=/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/71/fs,workdir=/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/71/work,xino=off)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev type tmpfs (rw,nosuid,size=65536k,mode=755)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=666)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)
sysfs on /sys type sysfs (ro,nosuid,nodev,noexec,relatime)
tmpfs on /sys/fs/cgroup type tmpfs (rw,nosuid,nodev,noexec,relatime,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (ro,nosuid,nodev,noexec,relatime,xattr,name=systemd)
cgroup on /sys/fs/cgroup/rdma type cgroup (ro,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/pids type cgroup (ro,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (ro,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/freezer type cgroup (ro,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/perf_event type cgroup (ro,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (ro,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/blkio type cgroup (ro,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (ro,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (ro,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (ro,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/cpuset type cgroup (ro,nosuid,nodev,noexec,relatime,cpuset)
tmpfs on /etc/secret2 type tmpfs (ro,relatime,size=1928540k)
/dev/vda1 on /etc/hosts type ext4 (rw,relatime)
/dev/vda1 on /dev/termination-log type ext4 (rw,relatime)
/dev/vda1 on /etc/hostname type ext4 (rw,relatime)
/dev/vda1 on /etc/resolv.conf type ext4 (rw,relatime)
shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,size=65536k)
tmpfs on /run/secrets/kubernetes.io/serviceaccount type tmpfs (ro,relatime,size=1928540k)
proc on /proc/bus type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/fs type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/irq type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/sys type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/sysrq-trigger type proc (ro,nosuid,nodev,noexec,relatime)
tmpfs on /proc/acpi type tmpfs (ro,relatime)
tmpfs on /proc/kcore type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /proc/keys type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /proc/timer_list type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /proc/sched_debug type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /proc/scsi type tmpfs (ro,relatime)
tmpfs on /sys/firmware type tmpfs (ro,relatime)
controlplane $ 
controlplane $ 
controlplane $ k exec pod pod -n restricted -- mount | grep secret2
tmpfs on /etc/secret2 type tmpfs (ro,relatime,size=1928540k)
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec pod pod -n restricted -- cat /etc/secret2    
cat: /etc/secret2: Is a directory
command terminated with exit code 1
controlplane $ k exec pod pod -n restricted -- cat /etc/secret2/secret2
cat: /etc/secret2/secret2: No such file or directory
command terminated with exit code 1
controlplane $ k exec pod pod -n restricted -- sh                      
controlplane $ k exec -it pod pod -n restricted -- sh
# 
# 
# 
# cd /etc/secret2/
# ls
password
# exit
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec pod pod -n restricted -- cat /etc/secret2/password
pass1234controlplane $ 
...







etcd way - 

controlplane $ ETCDCTL_API=3 etcdctl \
> --cacert=/etc/kubernetes/pki/etcd/ca.crt   \
>    --cert=/etc/kubernetes/pki/etcd/server.crt \
>    --key=/etc/kubernetes/pki/etcd/server.key  \
> get /registry/secrets/restricted/secret2
/registry/secrets/restricted/secret2
k8s


v1Secret

secret2
restricted"*$7f1a3913-b877-4bf9-8313-e16458954d452eB
kubectl-createUpdatevFieldsV1:1
/{"f:data":{".":{},"f:password":{}},"f:type":{}}B
passworpass1234Opaque"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ ETCDCTL_API=3 etcdctl --cacert=/etc/kubernetes/pki/etcd/ca.crt      --cert=/etc/kubernetes/pki/etcd/server.crt    --key=/etc/kubernetes/pki/etcd/server.key  get /registry/secrets/restricted/secret3
/registry/secrets/restricted/secret3
k8s


v1Secret

secret3
restricted"*$f29f6019-cdd5-435d-bcb1-2f5b81243a062`B
kubectl-createUpdatevFieldsV1:,
*{"f:data":{".":{},"f:new":{}},"f:type":{}}B
newsecretOpaque"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get secret secret3 -n restricted -o yaml
apiVersion: v1
data:
  new: c2VjcmV0
kind: Secret
metadata:
  creationTimestamp: "2024-12-21T08:41:33Z"
  name: secret3
  namespace: restricted
  resourceVersion: "2585"
  uid: f29f6019-cdd5-435d-bcb1-2f5b81243a06
type: Opaque
controlplane $ ETCDCTL_API=3 etcdctl --cacert=/etc/kubernetes/pki/etcd/ca.crt      --cert=/etc/kubernetes/pki/etcd/server.crt    --key=/etc/kubernetes/pki/etcd/server.key  get /registry/secrets/restricted/secret2
/registry/secrets/restricted/secret2
k8s


v1Secret

secret2
restricted"*$7f1a3913-b877-4bf9-8313-e16458954d452eB
kubectl-createUpdatevFieldsV1:1
/{"f:data":{".":{},"f:password":{}},"f:type":{}}B
passworpass1234Opaque"
controlplane $ ETCDCTL_API=3 etcdctl --cacert=/etc/kubernetes/pki/etcd/ca.crt      --cert=/etc/kubernetes/pki/etcd/server.crt    --key=/etc/kubernetes/pki/etcd/server.key  get /registry/secrets/restricted/secret1
/registry/secrets/restricted/secret1
k8s


v1Secret

secret1
restricted"*$9f9e7342-f50e-4b69-bac9-4092c28143482bB
kubectl-createUpdatevFieldsV1:.
,{"f:data":{".":{},"f:admin":{}},"f:type":{}}B
adminswapOpaque"
controlplane $ 