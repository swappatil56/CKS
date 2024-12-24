Network security policies

network policies are FW in kubernetes

implemented by cni

namespace level

restrict ingress and egress based on certain rules


pod to pod communication is enabled by default 

##########################################################


controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   10d   v1.31.0
node01         Ready    <none>          10d   v1.31.0
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kubectl run frontend --image nginx
pod/frontend created
controlplane $ kubectl run backend --image nginx
pod/backend created
controlplane $ kubectl expose pod frontend --port 80
service/frontend exposed
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kubectl expose pod backend --port 80
service/backend exposed
controlplane $ kubectl get pod,svc
NAME           READY   STATUS    RESTARTS   AGE
pod/backend    1/1     Running   0          47s
pod/frontend   1/1     Running   0          59s

NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
service/backend      ClusterIP   10.101.159.78    <none>        80/TCP    10s
service/frontend     ClusterIP   10.111.115.187   <none>        80/TCP    26s
service/kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP   10d
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kubectl exec frontend -- curl backend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   615  100   615    0     0   100k      0 --:--:-- --:--:-- --:--:--  300k
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
controlplane $ 





ontrolplane $ kubectl exec backend -- curl frontend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   615  100   615    0     0   197k      0 --:--:-- --:--:-- --:--:--  600k
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
controlplane $ 

######################################################################################################


apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
  namespace: default
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress



controlplane $ vi netpol.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kubectl apply -f netpol.yaml 
networkpolicy.networking.k8s.io/default-deny created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ kubectl exec backend -- curl frontend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0^C
controlplane $ kubectl exec frontend -- curl backend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0^C
controlplane $ 






controlplane $ cat ingress.yaml 
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: ingress
  namespace: default
spec:
  podSelector:
    matchLabels: 
      run: backend
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
         run: frontend


         
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat egress.yaml 
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: egress
  namespace: default
spec:
  podSelector:
    matchLabels: 
     run: frontend
  policyTypes:
  - Egress
  egress:
  - to:
    - podSelector:
        matchLabels:
          run: backend
controlplane $ 



# allows frontend pods to communicate with backend pods
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: frontend
  namespace: default
spec:
  podSelector:
    matchLabels:
      run: frontend
  policyTypes:
    - Egress
  egress:
    - to:
        - podSelector:
            matchLabels:
              run: backend