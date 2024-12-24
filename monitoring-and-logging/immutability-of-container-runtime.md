# Use startup probe to remove bash and touch from container

controlplane $ cat pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: immutable
  name: immutable
spec:
  containers:
  - image: httpd
    name: immutable
    resources: {}
    startupProbe:
      exec:
        command:
        - rm
        - /bin/bash
      initialDelaySeconds: 1
      periodSeconds: 5
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}




controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/immutable created
controlplane $ k exec -it immutable -- bash
error: Internal error occurred: Internal error occurred: error executing command in container: failed to exec in container: failed to start exec "f4883d7d8fad5a0cbf5c644b6a7b6455987a4583f0788ab8ae517e342c806655": OCI runtime exec failed: exec failed: unable to start container process: exec: "bash": executable file not found in $PATH: unknown
controlplane $ 
controlplane $ 


#################################################################################

# create pod security context to make file system read-only
   ensure some directories are still writable using emptydir



controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/immutable created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME        READY   STATUS   RESTARTS      AGE
immutable   0/1     Error    2 (21s ago)   23s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME        READY   STATUS   RESTARTS      AGE
immutable   0/1     Error    2 (24s ago)   26s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k logs immutable
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 192.168.1.8. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 192.168.1.8. Set the 'ServerName' directive globally to suppress this message
[Tue Dec 17 10:29:31.883164 2024] [core:error] [pid 1:tid 1] (30)Read-only file system: AH00099: could not create /usr/local/apache2/logs/httpd.pid.vAhR88
[Tue Dec 17 10:29:31.883236 2024] [core:error] [pid 1:tid 1] AH00100: httpd: could not log pid to file /usr/local/apache2/logs/httpd.pid
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k logs immutable
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 192.168.1.8. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 192.168.1.8. Set the 'ServerName' directive globally to suppress this message
[Tue Dec 17 10:30:02.963932 2024] [core:error] [pid 1:tid 1] (30)Read-only file system: AH00099: could not create /usr/local/apache2/logs/httpd.pid.YxJzpK
[Tue Dec 17 10:30:02.963990 2024] [core:error] [pid 1:tid 1] AH00100: httpd: could not log pid to file /usr/local/apache2/logs/httpd.pid
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ k delete pod immutable --force
Warning: Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.
pod "immutable" force deleted
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/immutable created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME        READY   STATUS    RESTARTS   AGE
immutable   1/1     Running   0          5s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat pod.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: immutable
  name: immutable
spec:
  containers:
  - image: httpd
    name: immutable
    resources: {}
    securityContext:
      readOnlyRootFilesystem: true
    volumeMounts:
    - mountPath: /usr/local/apache2/logs
      name: httpd-logs
  volumes:
  - name: httpd-logs
    emptyDir: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
controlplane $ 



#################################################################################



in docker world there is another type like

docker run --read-only --tmpfs /run my-container



#################################

Lab


Create a Pod named pod-ro in Namespace sun of image busybox:1.32.0 .

Make sure the container keeps running, like using sleep 1d .

The container root filesystem should be read-only.




k run pod-ro --image busybox:1.32.0 -n sun -o yaml --dry-run=client -- sleep 1d > pod.yaml



controlplane $ k apply -f pod.yaml 
pod/pod-ro created
controlplane $ 
controlplane $ 
controlplane $ cat pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  annotations:
    cni.projectcalico.org/containerID: 53cd843b664d140a185ab0e41441cbe98654602536f81a797d22a415765fcd53
    cni.projectcalico.org/podIP: 192.168.0.10/32
    cni.projectcalico.org/podIPs: 192.168.0.10/32
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"creationTimestamp":null,"labels":{"run":"pod-ro"},"name":"pod-ro","namespace":"sun"},"spec":{"containers":[{"args":["sleep","1d"],"image":"busybox:1.32.0","name":"pod-ro","resources":{},"securityContext":{"readOnlyRootFilesystem":true}}],"dnsPolicy":"ClusterFirst","restartPolicy":"Always"},"status":{}}
  creationTimestamp: "2024-12-17T11:02:07Z"
  labels:
    run: pod-ro
  name: pod-ro
  namespace: sun
  resourceVersion: "2994"
  uid: 81b9ccad-8af7-4a1e-beba-71ad3aefd8e8
spec:
  containers:
  - args:
    - sleep
    - 1d
    image: busybox:1.32.0
    imagePullPolicy: IfNotPresent
    name: pod-ro
    resources: {}
    securityContext:
      readOnlyRootFilesystem: true
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-m6r5d
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: controlplane
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-m6r5d
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2024-12-17T11:02:09Z"
    status: "True"
    type: PodReadyToStartContainers
  - lastProbeTime: null
    lastTransitionTime: "2024-12-17T11:02:07Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2024-12-17T11:02:09Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2024-12-17T11:02:09Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2024-12-17T11:02:07Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://9b9212ae7bcbc99ca7bb7fd41f960a2a7e05ec52663ebaf2cb4804e378a898fd
    image: docker.io/library/busybox:1.32.0
    imageID: docker.io/library/busybox@sha256:bde48e1751173b709090c2539fdf12d6ba64e88ec7a4301591227ce925f3c678
    lastState: {}
    name: pod-ro
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-12-17T11:02:08Z"
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-m6r5d
      readOnly: true
      recursiveReadOnly: Disabled
  hostIP: 172.30.1.2
  hostIPs:
  - ip: 172.30.1.2
  phase: Running
  podIP: 192.168.0.10
  podIPs:
  - ip: 192.168.0.10
  qosClass: BestEffort
  startTime: "2024-12-17T11:02:07Z"
controlplane $ 