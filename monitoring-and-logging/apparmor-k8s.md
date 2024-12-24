## apparmor on kubernetes

- container runtime needs support for apparmor
- apparmor needs install on every node
- apparmor profiles needs to be available on every node of the cluster
- apparmor profiles are specified per container level
  - done using annotations

## create pod which uses an apparmor profile


controlplane $ k run secure --image nginx -o yaml --dry-run=client > pod.yaml
controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
Warning: metadata.annotations[container.apparmor.security.beta.kubernetes.io/secure]: deprecated since v1.30; use the "appArmorProfile" field instead
pod/secure created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get po
NAME     READY   STATUS                 RESTARTS   AGE
secure   0/1     CreateContainerError   0          9s
controlplane $ 
controlplane $ k describe po secure
Name:             secure
Namespace:        default
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Wed, 18 Dec 2024 08:25:48 +0000
Labels:           run=secure
Annotations:      cni.projectcalico.org/containerID: 8b10b496d682a269b0aa104cae7ab013bb1c9774a5b7d4fb67213bb902cf2ed4
                  cni.projectcalico.org/podIP: 192.168.1.7/32
                  cni.projectcalico.org/podIPs: 192.168.1.7/32
                  container.apparmor.security.beta.kubernetes.io/secure: localhost/hello
Status:           Pending
IP:               192.168.1.7
IPs:
  IP:  192.168.1.7
Containers:
  secure:
    Container ID:   
    Image:          nginx
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       CreateContainerError
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-vxlbx (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-vxlbx:
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
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  19s                default-scheduler  Successfully assigned default/secure to node01
  Normal   Pulled     11s                kubelet            Successfully pulled image "nginx" in 7.369s (7.369s including waiting). Image size: 72099501 bytes.
  Normal   Pulling    10s (x2 over 18s)  kubelet            Pulling image "nginx"
  Warning  Failed     10s (x2 over 11s)  kubelet            Error: failed to get container spec opts: failed to generate apparmor spec opts: apparmor profile not found hello
  Normal   Pulled     10s                kubelet            Successfully pulled image "nginx" in 514ms (514ms including waiting). Image size: 72099501 bytes.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ vi /etc/apparmor.d/docker-nginx
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ apparmor_parser /etc/apparmor.d/docker-nginx    
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k delete po secure --force
Warning: Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.
pod "secure" force deleted
controlplane $ 
controlplane $ k apply -f pod.yaml 
Warning: metadata.annotations[container.apparmor.security.beta.kubernetes.io/secure]: deprecated since v1.30; use the "appArmorProfile" field instead
pod/secure created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME     READY   STATUS                 RESTARTS   AGE
secure   0/1     CreateContainerError   0          63s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME     READY   STATUS                 RESTARTS   AGE
secure   0/1     CreateContainerError   0          78s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k logs secure
Error from server (BadRequest): container "secure" in pod "secure" is waiting to start: CreateContainerError
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k describe pod secure
Name:             secure
Namespace:        default
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Wed, 18 Dec 2024 08:29:36 +0000
Labels:           run=secure
Annotations:      cni.projectcalico.org/containerID: 14aa834111735115f3a4a78d1984c4628e91a2fffcb3af0e5775a67d6e760c33
                  cni.projectcalico.org/podIP: 192.168.1.8/32
                  cni.projectcalico.org/podIPs: 192.168.1.8/32
                  container.apparmor.security.beta.kubernetes.io/secure: localhost/docker-nginx
Status:           Pending
IP:               192.168.1.8
IPs:
  IP:  192.168.1.8
Containers:
  secure:
    Container ID:   
    Image:          nginx
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       CreateContainerError
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-pkphm (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-pkphm:
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
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  92s                default-scheduler  Successfully assigned default/secure to node01
  Normal   Pulled     91s                kubelet            Successfully pulled image "nginx" in 535ms (535ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     90s                kubelet            Successfully pulled image "nginx" in 601ms (601ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     89s                kubelet            Successfully pulled image "nginx" in 448ms (448ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     74s                kubelet            Successfully pulled image "nginx" in 472ms (472ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     59s                kubelet            Successfully pulled image "nginx" in 543ms (543ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     43s                kubelet            Successfully pulled image "nginx" in 532ms (532ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     31s                kubelet            Successfully pulled image "nginx" in 547ms (547ms including waiting). Image size: 72099501 bytes.
  Normal   Pulled     17s                kubelet            Successfully pulled image "nginx" in 453ms (453ms including waiting). Image size: 72099501 bytes.
  Warning  Failed     16s (x8 over 91s)  kubelet            Error: failed to get container spec opts: failed to generate apparmor spec opts: apparmor profile not found docker-nginx
  Normal   Pulling    3s (x9 over 92s)   kubelet            Pulling image "nginx"
controlplane $ 