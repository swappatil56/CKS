https://kubernetes.io/docs/concepts/security/controlling-access/


use kubelet.conf as a kubeconfig

controlplane $ k get nodes -o wide
NAME           STATUS   ROLES           AGE     VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
controlplane   Ready    control-plane   5d19h   v1.31.0   172.30.1.2    <none>        Ubuntu 20.04.5 LTS   5.4.0-131-generic   containerd://1.7.13
node01         Ready    <none>          5d19h   v1.31.0   172.30.2.2    <none>        Ubuntu 20.04.5 LTS   5.4.0-131-generic   containerd://1.7.13
controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ k config view
apiVersion: v1
clusters: null
contexts: null
current-context: ""
kind: Config
preferences: {}
users: null
node01 $ 
node01 $ 
node01 $ 
node01 $ vi /etc/kubernetes/kubelet.conf 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ export KUBECONFIG=/etc/kubernetes/kubelet.conf 
node01 $ 
node01 $ 
node01 $ k config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://172.30.1.2:6443
  name: default-cluster
contexts:
- context:
    cluster: default-cluster
    namespace: default
    user: default-auth
  name: default-context
current-context: default-context
kind: Config
preferences: {}
users:
- name: default-auth
  user:
    client-certificate: /var/lib/kubelet/pki/kubelet-client-current.pem
    client-key: /var/lib/kubelet/pki/kubelet-client-current.pem
node01 $ 
node01 $ 
node01 $ 
node01 $ k get nodes
NAME           STATUS   ROLES           AGE     VERSION
controlplane   Ready    control-plane   5d19h   v1.31.0
node01         Ready    <none>          5d19h   v1.31.0
node01 $ 
node01 $ 
node01 $ 
node01 $ k get ns   
Error from server (Forbidden): namespaces is forbidden: User "system:node:node01" cannot list resource "namespaces" in API group "" at the cluster scope
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ k label node controlplane test=test 
Error from server (Forbidden): nodes "controlplane" is forbidden: node "node01" is not allowed to modify node "controlplane"
node01 $ 
node01 $ 
node01 $ 
node01 $ k label node node01 test=test 
node/node01 labeled
node01 $ 

###important - node admission control even forbids the label creation for self node to create some system labels

node01 $ k label node node01 node-restriction.kubernetes.io/test=yes
Error from server (Forbidden): nodes "node01" is forbidden: is not allowed to modify labels: node-restriction.kubernetes.io/test
node01 $ 