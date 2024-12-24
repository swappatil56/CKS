



Create a Pod named pod-ro in Namespace sun of image busybox:1.32.0 .

Make sure the container keeps running, like using sleep 1d .

The container root filesystem should be read-only.



controlplane $ k run pod-ro -n sun --image busybox:1.32.0 -o yaml --dry-run=client -- sleep 1d > pod.yaml
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi pod.yaml 
controlplane $ 

controlplane $ cat pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod-ro
  name: pod-ro
  namespace: sun
spec:
  containers:
  - args:
    - sleep
    - 1d
    image: busybox:1.32.0
    name: pod-ro
    resources: {}
    securityContext:
      readOnlyRootFilesystem: true
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
controlplane $ 


controlplane $ 
controlplane $ 
controlplane $ k apply -f pod.yaml 
pod/pod-ro created
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod
No resources found in default namespace.
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n sun
NAME     READY   STATUS    RESTARTS   AGE
pod-ro   1/1     Running   0          9s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec -it pod-ro -- sh
Error from server (NotFound): pods "pod-ro" not found
controlplane $ k exec -it pod-ro -n sun -- sh
/ # 
/ # 
/ # 
/ # 
/ # echo test > /root/test
sh: can't create /root/test: Read-only file system
/ # 
/ # 
/ # 
/ # exit
command terminated with exit code 1
controlplane $ 


##############################################################################################


The Deployment web4.0 in Namespace moon doesn't seem to work with readOnlyRootFilesystem .

Add an emptyDir volume to fix this.



controlplane $ k get deploy -n moon -o yaml
apiVersion: v1
items:
- apiVersion: apps/v1
  kind: Deployment
  metadata:
    annotations:
      deployment.kubernetes.io/revision: "2"
    creationTimestamp: "2024-12-19T05:39:46Z"
    generation: 2
    labels:
      app: web4.0
    name: web4.0
    namespace: moon
    resourceVersion: "3130"
    uid: f3a86831-03af-434a-adb4-9e38525c01e8
  spec:
    progressDeadlineSeconds: 600
    replicas: 2
    revisionHistoryLimit: 10
    selector:
      matchLabels:
        app: web4.0
    strategy:
      rollingUpdate:
        maxSurge: 25%
        maxUnavailable: 25%
      type: RollingUpdate
    template:
      metadata:
        creationTimestamp: null
        labels:
          app: web4.0
      spec:
        containers:
        - command:
          - sh
          - -c
          - date > /etc/date.log && sleep 1d
          image: busybox:1.32.0
          imagePullPolicy: IfNotPresent
          name: container
          resources: {}
          securityContext:
            readOnlyRootFilesystem: true
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
          volumeMounts:
          - mountPath: /etc
            name: cache-volume
        dnsPolicy: ClusterFirst
        restartPolicy: Always
        schedulerName: default-scheduler
        securityContext: {}
        terminationGracePeriodSeconds: 30
        volumes:
        - emptyDir: {}
          name: cache-volume
  status:
    availableReplicas: 2
    conditions:
    - lastTransitionTime: "2024-12-19T05:50:45Z"
      lastUpdateTime: "2024-12-19T05:50:45Z"
      message: Deployment has minimum availability.
      reason: MinimumReplicasAvailable
      status: "True"
      type: Available
    - lastTransitionTime: "2024-12-19T05:39:46Z"
      lastUpdateTime: "2024-12-19T05:50:45Z"
      message: ReplicaSet "web4.0-d698f69f5" has successfully progressed.
      reason: NewReplicaSetAvailable
      status: "True"
      type: Progressing
    observedGeneration: 2
    readyReplicas: 2
    replicas: 2
    updatedReplicas: 2
kind: List
metadata:
  resourceVersion: ""
controlplane $ 