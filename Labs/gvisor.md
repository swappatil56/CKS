



node01 $ cat class.yaml
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
  # The name the RuntimeClass will be referenced by.
  # RuntimeClass is a non-namespaced resource.
  name: gvisor 
# The name of the corresponding CRI configuration
handler: runsc
node01 $ 

controlplane $ cat pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: sec
  name: sec
spec:
  runtimeClassName: gvisor
  containers:
  - image: nginx:1.21.5-alpine
    name: sec
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
controlplane $ 


controlplane $ k apply -f class.yaml 
runtimeclass.node.k8s.io/gvisor created
controlplane $ 
controlplane $ k run sec --image nginx:1.21.5-alpine -o yaml --dry-run=client > pod.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/sec created
controlplane $ k exec sec -- dmesg | grep -i gvisor
[   0.000000] Starting gVisor...
controlplane $ k exec sec -- dmesg | grep -i gvisor
[   0.000000] Starting gVisor...
controlplane $ 




###########################################################################

Task weight: 4%
Use context: kubectl config use-context workload-prod

Team purple wants to run some of their workloads more secure. Worker node cluster1-node2 has container engine containerd already installed and its configured to support the runsc/gvisor runtime.

Create a RuntimeClass named gvisor with handler runsc.

Create a Pod that uses the RuntimeClass. The Pod should be in Namespace team-purple, named gvisor-test and of image nginx:1.19.2. Make sure the Pod runs on cluster1-node2.

Write the dmesg output of the successfully started Pod into /opt/course/10/gvisor-test-dmesg.


Ans->

controlplane $ k create ns team-purple
namespace/team-purple created
controlplane $ k run gvisor-test --image nginx:1.19.2 -n team-purple -o yaml --dry-run=client > pod123.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod123.yaml 
controlplane $ vi pod123.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod123.yaml 
pod/gvisor-test created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME   READY   STATUS    RESTARTS   AGE
sec    1/1     Running   0          6m18s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n team-purple
NAME          READY   STATUS              RESTARTS   AGE
gvisor-test   0/1     ContainerCreating   0          11s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n team-purple
NAME          READY   STATUS    RESTARTS   AGE
gvisor-test   1/1     Running   0          13s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec -it gvisor-test -- dmesg 
Error from server (NotFound): pods "gvisor-test" not found
controlplane $ 
controlplane $ 
controlplane $ k exec -it gvisor-test -- dmesg -n team-purple
Error from server (NotFound): pods "gvisor-test" not found
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec -it gvisor-test -n team-purple -- dmesg               
[    0.000000] Starting gVisor...
[    0.395225] Reticulating splines...
[    0.644101] Generating random numbers by fair dice roll...
[    1.089097] Checking naughty and nice process list...
[    1.506795] Granting licence to kill(2)...
[    1.840185] Feeding the init monster...
[    1.920862] Constructing home...
[    2.218927] Synthesizing system calls...
[    2.421589] Creating cloned children...
[    2.596720] Reading process obituaries...
[    2.612877] Gathering forks...
[    2.835819] Setting up VFS...
[    3.103687] Setting up FUSE...
[    3.471406] Ready!
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec -it gvisor-test -n team-purple -- dmesg > /opt/course/10/gvisor-test-dmesg
bash: /opt/course/10/gvisor-test-dmesg: No such file or directory
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ mkdir /opt/course/10
mkdir: cannot create directory '/opt/course/10': No such file or directory
controlplane $ 
controlplane $ 
controlplane $ mkdir -r /opt/course/10
mkdir: invalid option -- 'r'
Try 'mkdir --help' for more information.
controlplane $ 
controlplane $ mkdir -R /opt/course/10
mkdir: invalid option -- 'R'
Try 'mkdir --help' for more information.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -o wide  
NAME   READY   STATUS    RESTARTS   AGE     IP            NODE     NOMINATED NODE   READINESS GATES
sec    1/1     Running   0          8m25s   192.168.1.4   node01   <none>           <none>
controlplane $ 
controlplane $ 
controlplane $ 