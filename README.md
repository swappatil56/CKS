Certificates

there are below total internal certs are used in k8s architecture

1. CA crt
2. Api server cert
3. Etcd server cert
4. kubelete Server cert
5. api-> etcd
6. scheduler-> api
7. cloud controller -> api
8. controller manager -> api
9. kubelet -> api
10. api -> kubelet


controlplane $ cd /etc/kubernetes/pki/
controlplane $ ls -ltr
total 60
-rw------- 1 root root 1675 Nov  6 12:27 ca.key
-rw-r--r-- 1 root root 1107 Nov  6 12:27 ca.crt
-rw------- 1 root root 1675 Nov  6 12:27 apiserver.key
-rw-r--r-- 1 root root 1289 Nov  6 12:27 apiserver.crt
-rw------- 1 root root 1679 Nov  6 12:27 apiserver-kubelet-client.key
-rw-r--r-- 1 root root 1176 Nov  6 12:27 apiserver-kubelet-client.crt
-rw------- 1 root root 1675 Nov  6 12:27 front-proxy-ca.key
-rw-r--r-- 1 root root 1123 Nov  6 12:27 front-proxy-ca.crt
-rw------- 1 root root 1675 Nov  6 12:27 front-proxy-client.key
-rw-r--r-- 1 root root 1119 Nov  6 12:27 front-proxy-client.crt
drwxr-xr-x 2 root root 4096 Nov  6 12:27 etcd
-rw------- 1 root root 1675 Nov  6 12:27 apiserver-etcd-client.key
-rw-r--r-- 1 root root 1123 Nov  6 12:27 apiserver-etcd-client.crt
-rw------- 1 root root  451 Nov  6 12:27 sa.pub
-rw------- 1 root root 1675 Nov  6 12:27 sa.key

##################etcd certificates##########################################################################################

controlplane $ cd /etc/kubernetes/pki/
controlplane $ ls -ltr
total 60
-rw------- 1 root root 1675 Nov  6 12:27 ca.key
-rw-r--r-- 1 root root 1107 Nov  6 12:27 ca.crt
-rw------- 1 root root 1675 Nov  6 12:27 apiserver.key
-rw-r--r-- 1 root root 1289 Nov  6 12:27 apiserver.crt
-rw------- 1 root root 1679 Nov  6 12:27 apiserver-kubelet-client.key
-rw-r--r-- 1 root root 1176 Nov  6 12:27 apiserver-kubelet-client.crt
-rw------- 1 root root 1675 Nov  6 12:27 front-proxy-ca.key
-rw-r--r-- 1 root root 1123 Nov  6 12:27 front-proxy-ca.crt
-rw------- 1 root root 1675 Nov  6 12:27 front-proxy-client.key
-rw-r--r-- 1 root root 1119 Nov  6 12:27 front-proxy-client.crt
-rw------- 1 root root 1675 Nov  6 12:27 apiserver-etcd-client.key
-rw-r--r-- 1 root root 1123 Nov  6 12:27 apiserver-etcd-client.crt
-rw------- 1 root root  451 Nov  6 12:27 sa.pub
-rw------- 1 root root 1675 Nov  6 12:27 sa.key
drwxr-xr-x 3 root root 4096 Nov 16 06:54 etcd
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd etcd
controlplane $ ls
ca.crt  ca.key  healthcheck-client.crt  healthcheck-client.key  peer.crt  peer.key  server.crt  server.key
controlplane $ ls -ltr
total 32
-rw------- 1 root root 1679 Nov  6 12:27 ca.key
-rw-r--r-- 1 root root 1094 Nov  6 12:27 ca.crt
-rw------- 1 root root 1675 Nov  6 12:27 server.key
-rw-r--r-- 1 root root 1208 Nov  6 12:27 server.crt
-rw------- 1 root root 1679 Nov  6 12:27 peer.key
-rw-r--r-- 1 root root 1208 Nov  6 12:27 peer.crt
-rw------- 1 root root 1675 Nov  6 12:27 healthcheck-client.key
-rw-r--r-- 1 root root 1123 Nov  6 12:27 healthcheck-client.crt
controlplane $ 

###########Kubelet certificates####################################

controlplane $ cd /etc/kubernetes/
controlplane $ ls -ltr
total 44
drwxr-xr-x 3 root root 4096 Nov  6 12:27 pki
-rw------- 1 root root 5654 Nov  6 12:27 admin.conf
-rw------- 1 root root 5674 Nov  6 12:27 super-admin.conf
-rw------- 1 root root 5678 Nov  6 12:27 controller-manager.conf
-rw------- 1 root root 5622 Nov  6 12:27 scheduler.conf
-rw------- 1 root root 1990 Nov  6 12:28 kubelet.conf
drwxrwxr-x 2 root root 4096 Nov  6 12:29 manifests
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat kubelet.conf 
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJVGRQeG5YUlh6R0V3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFeE1EWXhNakl5TkROYUZ3MHpOREV4TURReE1qSTNORE5hTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUURiSmMweDBNS3JXZmo2Rk9hSTlvVUttTWd0UFJJTFhheW0vS08xTXY1Qm1OUml0eVRlU3ovSGZGYzUKaSt6SXd5Mk5BbVR6Q2xMeWFTbE0vZ3ZBb2szMVhNaThZSERBU1hZTDdXa1B0L3VsNHBqTURwSmFQTy9rSnl5QgpvT3JsRlczSklRTFQ2em4yM2tpQW96b1FTR2l6MnlhNHEyM0tTTjRPODBMQTFmNzVFT0psWnNnMk9aUklHNmZLCkY4U0hGdUxaakRmNUljMHhuUktsc0NsWjlYYnNKS3huUzc3YXoxU3RCWm1GUGplK3BYSXlpeVdicnY1V3VuWXcKZ2NpVjhYL1ZKN0M4cjFqT1RrYUYwYTdIWGdvYzZ6RUVETTB1bkhaeEw4aWppcW1JL1FVUVlPWVNmWDQ0ankwVAoxQUFBWmZkYlNjeVliTXJJU0FsallJWlZNeWJqQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJSZ2gybGs0OGUxK3h5MjZBQzd1UEt3NTkxNmNqQVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQnFlM2ZwU2dhbwpSTEM3eVBSem9UMTRqalAzNDR5OVBoK0tFay9MY2dDQnU5Y2ZxOTg2Zi9keWpyekdUNTY1QmloVWZRckZ0UWVOCmtTbnlEbFZlaHFua2d1NUlqYVp2MkViL1czQlhUc1R6VEx1dHdRRmVRenRPdC80VXFjcmRrb0pKYWUxSk5nd2gKdkZZNkozc0NIc3ZuZkNQb043RkdubjZhSExYckxRZVBDcEI5Ym5LWWUzQUJvSjllT3V4Y3FPd1QxYldIWkdoZQpIWFJsTmc0bG5kdTgrM1dBcUtMa1ljdmVqQks2aU9QcFBOZHpsemZZRTFGamVhRHFrZUlHaFU5QWxnYTRnNnRkClBqT0hOMXViS1RuVWZreHNHekNRcUF0UnRCbXlUQ3pjMEkzK3JsdDVvenI2eWdFTHNNbmJpa0RZNzgzQSsrU0QKT3pCR21xWS9EYWJOCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://172.30.1.2:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: system:node:controlplane
  name: system:node:controlplane@kubernetes
current-context: system:node:controlplane@kubernetes
kind: Config
preferences: {}
users:
- name: system:node:controlplane
  user:
    client-certificate: /var/lib/kubelet/pki/kubelet-client-current.pem
    client-key: /var/lib/kubelet/pki/kubelet-client-current.pem
controlplane $ 



controlplane $ cd /var/lib/kubelet/pki/
controlplane $ ls -ltr
total 12
-rw------- 1 root root 1679 Nov  6 12:27 kubelet.key
-rw-r--r-- 1 root root 2295 Nov  6 12:27 kubelet.crt
lrwxrwxrwx 1 root root   59 Nov  6 12:27 kubelet-client-current.pem -> /var/lib/kubelet/pki/kubelet-client-2024-11-06-12-27-58.pem
-rw------- 1 root root 2830 Nov  6 12:27 kubelet-client-2024-11-06-12-27-58.pem
controlplane $ 

#######################################################################################################################################################################################

