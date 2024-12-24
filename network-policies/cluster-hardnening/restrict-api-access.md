https://kubernetes.io/docs/concepts/security/controlling-access/




Authentication & Authorization Admission
Connect to API in different ways
Restrict API access in various ways




##Authentication & Authorization Admission

Authentication -> who are you?

Authorization -> are you even allowed to do action?


Admission controller -> limits of pods has been reached? opa validate domain and all.... write your own policies


##########
Api request should always tied to -

User
Service account
anonymous request

every request must be authenticate or be treated as anonymous requests

####################
Restriction->

1. dont allow anonymous access

   kube-apiserver --anonymous-auth=true/false


2. close insecure port
3. don't expose api server to outside
4. restrict access from nodes to api (node restriction)
5. prevent unauthorized access (RBAC)
6. prevent pods from acccessing api
7. Api server port behind firewall/ allowed ip ranges(cloud provider)


###############################################################################


enable and disable anonymous access and test

controlplane $ cd /etc/kubernetes/
controlplane $ ls
admin.conf  controller-manager.conf  kubelet.conf  manifests  pki  scheduler.conf  super-admin.conf
controlplane $ cd manifests/
controlplane $ ls -ltr
total 16
-rw------- 1 root root 3393 Dec  6 09:15 kube-controller-manager.yaml
-rw------- 1 root root 3871 Dec  6 09:15 kube-apiserver.yaml
-rw------- 1 root root 1462 Dec  6 09:15 kube-scheduler.yaml
-rw------- 1 root root 2534 Dec  6 09:15 etcd.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ curl https://localhost:6443
curl: (60) SSL certificate problem: unable to get local issuer certificate
More details here: https://curl.haxx.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
controlplane $ curl https://localhost:6443 -k
{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {},
  "status": "Failure",
  "message": "forbidden: User \"system:anonymous\" cannot get path \"/\"",
  "reason": "Forbidden",
  "details": {},
  "code": 403
}controlplane $ 



apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubeadm.kubernetes.io/kube-apiserver.advertise-address.endpoint: 172.30.1.2:6443
  creationTimestamp: null
  labels:
    component: kube-apiserver
    tier: control-plane
  name: kube-apiserver
  namespace: kube-system
spec:
  containers:
  - command:
    - kube-apiserver
    - --anonymous-auth=false
    - --advertise-address=172.30.1.2
    - --allow-privileged=true
    - --authorization-mode=Node,RBAC


##################################################################


make kubernetes api reachable from outside

1. expose clusterip to nodeport
2. curl -kvv https://172.30.2.2:31110

3. copy kubeconfig to local
4. k --kubeconfig  conf get ns

