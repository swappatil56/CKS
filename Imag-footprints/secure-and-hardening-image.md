
https://docs.docker.com/develop/develop-images/dockerfile_best-practices

############Secure and Hardening Images#################

1. Use Specific Image version FROM alpine:3.20.3

controlplane $ cat Dockerfile 
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

FROM alpine:3.20.3    #Specific Image version alpine:3.20.3 has been used so that container will not get restarts every time and make issues in productions as well
COPY --from=0 /app .
CMD ["./app"]
controlplane $ 



controlplane $ docker build -t app .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/
Sending build context to Docker daemon  3.671MB
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
Step 6/8 : FROM alpine:3.20.3
3.20.3: Pulling from library/alpine
da9db072f522: Pull complete 
Digest: sha256:1e42bbe2508154c9126d48c2b8a75420c3544343bf86fd041fb7527e017a4b4a
Status: Downloaded newer image for alpine:3.20.3
 ---> 63b790fccc90
Step 7/8 : COPY --from=0 /app .
 ---> 243983989a4e
Step 8/8 : CMD ["./app"]
 ---> Running in ebd9633729ac
Removing intermediate container ebd9633729ac
 ---> de7ccacdab3e
Successfully built de7ccacdab3e
Successfully tagged app:latest
controlplane $ 


################################################################################################################

2. Don't run as Root

controlplane $ vi Dockerfile 
controlplane $ 


controlplane $ cat Dockerfile 



FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

FROM alpine:3.20.3
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser  # app user 
COPY --from=0 /app /home/appuser
CMD ["/home/appuser/app"]
controlplane $ 



ontrolplane $ vi Dockerfile 
controlplane $ 
controlplane $ 
controlplane $ cat Dockerfile 
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

FROM alpine:3.20.3
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser 
COPY --from=0 /app /home/appuser
USER appuser
CMD ["/home/appuser/app"]
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker build -t app .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  3.674MB
Step 1/10 : FROM ubuntu
 ---> b1d9df8ab815
Step 2/10 : ARG DEBIAN_FRONTEND=noninteractive
 ---> Using cache
 ---> f8dd63b1352e
Step 3/10 : RUN apt-get update && apt-get install -y golang-go
 ---> Using cache
 ---> 779e9b80b6e0
Step 4/10 : COPY app.go .
 ---> Using cache
 ---> af1f855853fe
Step 5/10 : RUN CGO_ENABLED=0 go build app.go
 ---> Using cache
 ---> 645ec8b2ed7a
Step 6/10 : FROM alpine:3.20.3
 ---> 63b790fccc90
Step 7/10 : RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
 ---> Running in 72a6bf97beb5
Removing intermediate container 72a6bf97beb5
 ---> 9c790de700a8
Step 8/10 : COPY --from=0 /app /home/appuser
 ---> 97e0f79fc15e
Step 9/10 : USER appuser
 ---> Running in c9a1a6acaef4
Removing intermediate container c9a1a6acaef4
 ---> a4eb3520333e
Step 10/10 : CMD ["/home/appuser/app"]
 ---> Running in 7d3962b16a19
Removing intermediate container 7d3962b16a19
 ---> 88671a91f831
Successfully built 88671a91f831
Successfully tagged app:latest
controlplane $ 



controlplane $ docker run app
user: appuser id: 100
user: appuser id: 100
user: appuser id: 100
user: appuser id: 100
^Cuser: appuser id: 100
################################################################################################################


3. Make filesystem read only

controlplane $ vi Dockerfile 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat Dockerfile 
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

FROM alpine:3.20.3
RUN chmod a-w /etc
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
COPY --from=0 /app /home/appuser
USER appuser
CMD ["/home/appuser/app"]
controlplane $ 

controlplane $ docker build -t app .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent to tar: archive/tar: sockets not supported 
ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent.browser to tar: archive/tar: sockets not supported 
ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent.extra to tar: archive/tar: sockets not supported 
ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent.ssh to tar: archive/tar: sockets not supported 
Sending build context to Docker daemon  3.674MB
Step 1/11 : FROM ubuntu
 ---> b1d9df8ab815
Step 2/11 : ARG DEBIAN_FRONTEND=noninteractive
 ---> Using cache
 ---> f8dd63b1352e
Step 3/11 : RUN apt-get update && apt-get install -y golang-go
 ---> Using cache
 ---> 779e9b80b6e0
Step 4/11 : COPY app.go .
 ---> Using cache
 ---> af1f855853fe
Step 5/11 : RUN CGO_ENABLED=0 go build app.go
 ---> Using cache
 ---> 645ec8b2ed7a
Step 6/11 : FROM alpine:3.20.3
 ---> 63b790fccc90
Step 7/11 : RUN chmod a-w /etc
 ---> Running in d508dfa29e5a
Removing intermediate container d508dfa29e5a
 ---> d002a64f5fec
Step 8/11 : RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
 ---> Running in e1ba4fcb3c56
Removing intermediate container e1ba4fcb3c56
 ---> fb584ac51f6b
Step 9/11 : COPY --from=0 /app /home/appuser
 ---> c0d6d3388296
Step 10/11 : USER appuser
 ---> Running in d7ddcd13b652
Removing intermediate container d7ddcd13b652
 ---> 095b9414514f
Step 11/11 : CMD ["/home/appuser/app"]
 ---> Running in 1a9a33fc0d7d
Removing intermediate container 1a9a33fc0d7d
 ---> 630497e864b1
Successfully built 630497e864b1
Successfully tagged app:latest
controlplane $ 


controlplane $ docker run -d app
732cf3de6b33ad554f5f90eb27ea7a0023652986e2767205d5cc93fb43bfd843
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker exec -it 732cf3de6b33ad554f5f90eb27ea7a0023652986e2767205d5cc93fb43bfd843
"docker exec" requires at least 2 arguments.
See 'docker exec --help'.

Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Execute a command in a running container
controlplane $ 
controlplane $ 
controlplane $ docker exec -it 732cf3de6b33ad554f5f90eb27ea7a0023652986e2767205d5cc93fb43bfd843 sh
/ $ 
/ $ 
/ $ ls -ltr
total 60
drwxr-xr-x   12 root     root          4096 Sep  6 11:34 var
drwxr-xr-x    7 root     root          4096 Sep  6 11:34 usr
drwxrwxrwt    2 root     root          4096 Sep  6 11:34 tmp
drwxr-xr-x    2 root     root          4096 Sep  6 11:34 srv
drwxr-xr-x    2 root     root          4096 Sep  6 11:34 run
drwx------    2 root     root          4096 Sep  6 11:34 root
drwxr-xr-x    2 root     root          4096 Sep  6 11:34 opt
drwxr-xr-x    2 root     root          4096 Sep  6 11:34 mnt
drwxr-xr-x    5 root     root          4096 Sep  6 11:34 media
drwxr-xr-x    6 root     root          4096 Sep  6 11:34 lib
drwxr-xr-x    2 root     root          4096 Sep  6 11:34 sbin
drwxr-xr-x    2 root     root          4096 Sep  6 11:34 bin
drwxr-xr-x    1 root     root          4096 Dec 16 06:24 home
dr-xr-xr-x   13 root     root             0 Dec 16 06:25 sys
dr-xr-xr-x  266 root     root             0 Dec 16 06:25 proc
dr-xr-xr-x    1 root     root          4096 Dec 16 06:25 etc
drwxr-xr-x    5 root     root           340 Dec 16 06:25 dev
/ $ 



##############################################################################################################

4. remove shell access


controlplane $ vi Dockerfile 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker build -t app .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent to tar: archive/tar: sockets not supported 
ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent.browser to tar: archive/tar: sockets not supported 
ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent.extra to tar: archive/tar: sockets not supported 
ERRO[0000] Can't add file /root/.gnupg/S.gpg-agent.ssh to tar: archive/tar: sockets not supported 
Sending build context to Docker daemon  3.674MB
Step 1/12 : FROM ubuntu
 ---> b1d9df8ab815
Step 2/12 : ARG DEBIAN_FRONTEND=noninteractive
 ---> Using cache
 ---> f8dd63b1352e
Step 3/12 : RUN apt-get update && apt-get install -y golang-go
 ---> Using cache
 ---> 779e9b80b6e0
Step 4/12 : COPY app.go .
 ---> Using cache
 ---> af1f855853fe
Step 5/12 : RUN CGO_ENABLED=0 go build app.go
 ---> Using cache
 ---> 645ec8b2ed7a
Step 6/12 : FROM alpine:3.20.3
 ---> 63b790fccc90
Step 7/12 : RUN chmod a-w /etc
 ---> Using cache
 ---> d002a64f5fec
Step 8/12 : RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
 ---> Using cache
 ---> fb584ac51f6b
Step 9/12 : RUN rm -rf /bin/*
 ---> Running in c08381e0fc76
Removing intermediate container c08381e0fc76
 ---> 65e1c1326cec
Step 10/12 : COPY --from=0 /app /home/appuser
 ---> 49cfc7726327
Step 11/12 : USER appuser
 ---> Running in db1fa2c9e21e
Removing intermediate container db1fa2c9e21e
 ---> bd533ba8ea56
Step 12/12 : CMD ["/home/appuser/app"]
 ---> Running in 13a28461859c
Removing intermediate container 13a28461859c
 ---> 2821bf9ede34
Successfully built 2821bf9ede34
Successfully tagged app:latest
controlplane $ 


controlplane $ cat Dockerfile 
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

FROM alpine:3.20.3
RUN chmod a-w /etc
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
RUN rm -rf /bin/*
COPY --from=0 /app /home/appuser
USER appuser
CMD ["/home/appuser/app"]
controlplane $ 



controlplane $ docker run -d app 
a9cdc8c1faa41bb8a54b6172a170e1bbf65f510fdd4c3bd744aa763be9746e51
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker exec a9cdc8c1faa41bb8a54b6172a170e1bbf65f510fdd4c3bd744aa763be9746e51 -it sh
OCI runtime exec failed: exec failed: unable to start container process: exec: "-it": executable file not found in $PATH: unknown



##############################################################################################################