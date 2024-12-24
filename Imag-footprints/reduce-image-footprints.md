# Multi stage build

controlplane $ k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   9d    v1.31.0
node01         Ready    <none>          9d    v1.31.0
controlplane $ vi Dockerfile 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi app.go
controlplane $ ls -ltr
total 12
lrwxrwxrwx 1 root root    1 Dec  6 09:07 filesystem -> /
drwx------ 3 root root 4096 Dec  6 09:12 snap
-rw-r--r-- 1 root root  160 Dec 16 05:30 Dockerfile
-rw-r--r-- 1 root root  275 Dec 16 05:30 app.go
controlplane $ vi Dockerfile 
controlplane $ docker build -t app .

Setting up libheif-plugin-aomenc:amd64 (1.17.6-1ubuntu4.1) ...
Processing triggers for libc-bin (2.39-0ubuntu8.3) ...


Removing intermediate container 08afb1ea1214
 ---> 779e9b80b6e0
Step 4/6 : COPY app.go .
 ---> af1f855853fe
Step 5/6 : RUN CGO_ENABLED=0 go build app.go
 ---> Running in cf4e304f8b7a

Removing intermediate container cf4e304f8b7a
 ---> 645ec8b2ed7a
Step 6/6 : CMD ["./app"]
 ---> Running in d412e203406d
Removing intermediate container d412e203406d
 ---> 49f403a9ab88
Successfully built 49f403a9ab88
Successfully tagged app:latest
controlplane $ 



controlplane $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
app          latest    49f403a9ab88   36 seconds ago   636MB
ubuntu       latest    b1d9df8ab815   3 weeks ago      78.1MB
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker run app
user: root id: 0
user: root id: 0
user: root id: 0
user: root id: 0
user: root id: 0


controlplane $ docker image list
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
app          latest    49f403a9ab88   About a minute ago   636MB
ubuntu       latest    b1d9df8ab815   3 weeks ago          78.1MB
controlplane $ 


#####task reduce image size by reducing the stpes


cat Dockerfile


FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go
CMD ["./app"]
~      






with changes - 

controlplane $ vi Dockerfile 
controlplane $ 

controlplane $ cat Dockerfile 

#layer 0 
FROM ubuntu                                      
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

#layer 1
FROM alpine
COPY --from=0 /app .  # calls app folder from layer 0 container and copy here in current stage of container
CMD ["./app"]
controlplane $ 



controlplane $ docker build -t app .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/
Sending build context to Docker daemon  3.668MB
Step 1/8 : FROM ubuntu
 ---> b1d9df8ab815
Step 2/8 : ARG DEBIAN_FRONTEND=noninteractive
 ---> Using cache
 ---> f8dd63b1352e
Step 3/8 : RUN apt-get update && apt-get install -y golang-go
 ---> Using cache
 ---> 779e9b80b6e0
Step 4/8 : COPY app.go .
 ---> Using cache
 ---> af1f855853fe
Step 5/8 : RUN CGO_ENABLED=0 go build app.go
 ---> Using cache
 ---> 645ec8b2ed7a
Step 6/8 : FROM alpine
latest: Pulling from library/alpine
38a8310d387e: Pull complete 
Digest: sha256:21dc6063fd678b478f57c0e13f47560d0ea4eeba26dfc947b2a4f81f686b9f45
Status: Downloaded newer image for alpine:latest
 ---> 4048db5d3672
Step 7/8 : COPY --from=0 /app .
 ---> c2c4302091f0
Step 8/8 : CMD ["./app"]
 ---> Running in a0cb58d9cd76
Removing intermediate container a0cb58d9cd76
 ---> 0228bda8af76
Successfully built 0228bda8af76
Successfully tagged app:latest
controlplane $ 



controlplane $ docker run app
user: root id: 0
user: root id: 0
user: root id: 0
user: root id: 0



controlplane $ docker image list
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
app          latest    0228bda8af76   About a minute ago   9.86MB   # 9mb
<none>       <none>    49f403a9ab88   10 minutes ago       636MB
alpine       latest    4048db5d3672   10 days ago          7.84MB
ubuntu       latest    b1d9df8ab815   3 weeks ago          78.1MB
controlplane $ 