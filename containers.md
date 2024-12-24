Containers and Images

#Dockerfile -> script or text which defines how to build an image 
------> Docker build(which build image from docker file) multilayer binary represent state
        -----> Docker run container (running instance of image)
               -------> Docker push to repo like docker registry of artifactory


 What is container?

 Its collection of one or multiple applications and bundled there all dependencies runs on linux kernel however we can not see bez of encpasulation in pod.

 container is instanciation of the image.
##############################################################################################################


Container tools

docker, containerd, podman & crictl

docker -> manage container, images & container runtime
containerd -> container runtime also replacing docker in k8s from version 1.22
podman -> managing container and images 
crictl -> cli for cri compatible runtime


controlplane $ cat Dockerfile
FROM bash
CMD ["PING", "killer.sh"]
controlplane $ docker build -t test .
Sending build context to Docker daemon  3.631MB
Step 1/2 : FROM bash
 ---> 0d8232586933
Step 2/2 : CMD ["PING", "killer.sh"]
 ---> Using cache
 ---> 4242819d9f87
Successfully built 4242819d9f87
Successfully tagged test:latest
controlplane $ 



controlplane $ docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
test         latest    4242819d9f87   About a minute ago   14.4MB
bash         latest    0d8232586933   7 weeks ago          14.4MB
controlplane $ 


controlplane $ docker run test
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: seq=0 ttl=106 time=2.576 ms
64 bytes from 8.8.8.8: seq=1 ttl=106 time=2.562 ms
64 bytes from 8.8.8.8: seq=2 ttl=106 time=2.535 ms
64 bytes from 8.8.8.8: seq=3 ttl=106 time=2.526 ms
64 bytes from 8.8.8.8: seq=4 ttl=106 time=2.536 ms
64 bytes from 8.8.8.8: seq=5 ttl=106 time=2.585 ms
64 bytes from 8.8.8.8: seq=6 ttl=106 time=2.497 ms


controlplane $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
controlplane $ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                       PORTS     NAMES
810c7bc1ba7a   test           "docker-entrypoint.s…"   2 minutes ago   Exited (0) 2 minutes ago               peaceful_gould
bdb3ec8daef0   0a99b0280178   "docker-entrypoint.s…"   2 minutes ago   Exited (127) 2 minutes ago             pedantic_gould
3ea8e06fd36b   4242819d9f87   "docker-entrypoint.s…"   4 minutes ago   Exited (127) 4 minutes ago             intelligent_chebyshev
controlplane $ 



controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
ec34e552dcfb1       95fef08b8bf89       10 minutes ago      Running             local-path-provisioner    2                   5fabf0e9c126f       local-path-provisioner-6c5cff8948-tbl5l
92ba115d9c57e       f9c3c1813269c       11 minutes ago      Running             calico-kube-controllers   2                   413076eeea346       calico-kube-controllers-94fb6bc47-zb75s
0babb9408a62b       e6ea68648f0cd       11 minutes ago      Running             kube-flannel              1                   cf62d27847e5d       canal-8px9n
d697d2aefbbef       75392e3500e36       11 minutes ago      Running             calico-node               1                   cf62d27847e5d       canal-8px9n
dfe37413f1283       ad83b2ca7b09e       11 minutes ago      Running             kube-proxy                2                   ae18f9bdf63f4       kube-proxy-ldvw7
1f236e3892ef9       2e96e5913fc06       11 minutes ago      Running             etcd                      2                   8f582e234bb55       etcd-controlplane
1c6856bac1f63       045733566833c       11 minutes ago      Running             kube-controller-manager   2                   38da2d397d330       kube-controller-manager-controlplane
d4598bc928d7f       1766f54c897f0       11 minutes ago      Running             kube-scheduler            2                   e811547759466       kube-scheduler-controlplane
1338b2915dcd0       604f5db92eaa8       11 minutes ago      Running             kube-apiserver            2                   73496458f1046       kube-apiserver-controlplane
controlplane $ 

#####crictl is configured for container runtime from 1.22 onwrards

we use crictl to communicate with containerd

controlplane $ cat /etc/crictl.yaml 
runtime-endpoint: unix:///run/containerd/containerd.sock
controlplane $ 

##############################################################################################################

Docker Isolation in action


controlplane $ docker run --name c1 -d ubuntu sh -c "sleep 1d" 
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
afad30e59d72: Pull complete 
Digest: sha256:278628f08d4979fb9af9ead44277dbc9c92c2465922310916ad0c46ec9999295
Status: Downloaded newer image for ubuntu:latest
05f1052b61d63c8b101ec8e71c04cd69efed38177581afb3254d67d4d889a7ce
controlplane $ 
controlplane $


controlplane $ docker exec c1 ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   2792  1136 ?        Ss   11:26   0:00 sh -c sleep 1d
root           6  0.0  0.0   2688  1016 ?        S    11:26   0:00 sleep 1d
root           7 33.3  0.1   7880  3732 ?        Rs   11:27   0:00 ps aux
controlplane $ 


controlplane $ docker run --name c2 -d ubuntu sh -c "sleep 2d" 
3345c3d2e99c9c70e7feb85d972ba0cb5aadbc314827e32a9819f93359ec5033
controlplane $ docker exec c2 ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   2792  1144 ?        Ss   11:28   0:00 sh -c sleep 2d
root           6  0.0  0.0   2688  1072 ?        S    11:28   0:00 sleep 2d
root           7 50.0  0.1   7880  3960 ?        Rs   11:28   0:00 ps aux
controlplane $ 


host system o/p

controlplane $ ps aux | grep sleep
root        1546  0.0  0.0   3896  2004 ?        SN   11:10   0:00 bash -c set -x; cd /opt; while ! curl -o theia-install.sh https://storage.googleapis.com/killercoda-prod-europe1/theia/theia-install.sh?v=3370; do sleep 1; done; bash theia-install.sh; rm theia-install.sh; nice -n 19 /opt/theia/node /opt/theia/browser-app/src-gen/backend/main.js /root --hostname=0.0.0.0 --port 40205
root       13100  0.0  0.0   2792  1136 ?        Ss   11:26   0:00 sh -c sleep 1d
root       13129  0.0  0.0   2688  1016 ?        S    11:26   0:00 sleep 1d
root       13948  0.0  0.0   2792  1144 ?        Ss   11:28   0:00 sh -c sleep 2d
root       13970  0.0  0.0   2688  1072 ?        S    11:28   0:00 sleep 2d
root       14382  0.0  0.0   3304   724 pts/0    S+   11:28   0:00 grep --color=auto sleep
controlplane $ 



controlplane $ docker rm c2 --force
c2
controlplane $ docker run --name c2 --pid=container:c1 -d ubuntu sh -c "sleep 2d" 
fe94fc68b1e194d2ac40f207f1c00fcd6545a7c957bdbd594354ecd2fbac9513
controlplane $ docker exec c2 ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   2792  1136 ?        Ss   11:26   0:00 sh -c sleep 1d
root           6  0.0  0.0   2688  1016 ?        S    11:26   0:00 sleep 1d
root          13  0.0  0.0   2792  1072 ?        Ss   11:30   0:00 sh -c sleep 2d
root          18  0.0  0.0   2688  1080 ?        S    11:30   0:00 sleep 2d
root          19 50.0  0.1   7880  3940 ?        Rs   11:30   0:00 ps aux
controlplane $ 



controlplane $ docker exec c1 ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   2792  1136 ?        Ss   11:26   0:00 sh -c sleep 1d
root           6  0.0  0.0   2688  1016 ?        S    11:26   0:00 sleep 1d
root          13  0.0  0.0   2792  1072 ?        Ss   11:30   0:00 sh -c sleep 2d
root          18  0.0  0.0   2688  1080 ?        S    11:30   0:00 sleep 2d
root          24 33.3  0.1   7880  3924 ?        Rs   11:31   0:00 ps aux
controlplane $ 