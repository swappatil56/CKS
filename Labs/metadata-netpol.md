Use context: kubectl config use-context infra-prod

There is a metadata service available at http://192.168.100.21:32000 on which Nodes can reach sensitive data, like cloud credentials for initialisation. By default, all Pods in the cluster also have access to this endpoint. The DevSecOps team has asked you to restrict access to this metadata server.

In Namespace metadata-access:

Create a NetworkPolicy named metadata-deny which prevents egress to 192.168.100.21 for all Pods but still allows access to everything else

Create a NetworkPolicy named metadata-allow which allows Pods having label role: metadata-accessor to access endpoint 192.168.100.21

There are existing Pods in the target Namespace with which you can test your policies, but don't change their labels.



controlplane $ cat netpol.yaml 
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: metadata-deny
  namespace: metadata-access
spec:
  podSelector: {}
  policyTypes:
  - Egress
  egress:
   - to:
      - ipBlock:
           cidr: 0.0.0.0/0
           except:
            - 192.168.100.21/32

controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat nbetpol2.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: metadata-allow
  namespace: metadata-access
spec:
  podSelector:
    matchLabels:
      role: metadata-accessor
  policyTypes:
    - Egress
  egress:
    - to:
        - ipBlock:
            cidr: 192.168.100.21/32
controlplane $ 