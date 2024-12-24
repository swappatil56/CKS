Run two Docker containers app1 and app2 with the following attributes:

they should run image nginx:alpine

they should share the same PID kernel namespace

they should run command sleep infinity

they should run in the background (detached)

Then check which container sees which processes and make sense of why.



controlplane $ docker run --name app1 -d nginx:alpine sleep infinity
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
da9db072f522: Pull complete 
e10e486de1ab: Pull complete 
af9c0e53c5a4: Pull complete 
b2eb2b8af93a: Pull complete 
e351ee5ec3d4: Pull complete 
fbbf7d28be71: Pull complete 
471412c08d15: Pull complete 
a2eb5282fbec: Pull complete 
Digest: sha256:41523187cf7d7a2f2677a80609d9caa14388bf5c1fbca9c410ba3de602aaaab4
Status: Downloaded newer image for nginx:alpine
419f4defb489f74f7fb16a5029fcf24d77bc780d33b8cdb5256c5e91bca8c036
controlplane $ 


controlplane $ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS                      PORTS     NAMES
9de81346f92e   nginx:alpine   "/docker-entrypoint.…"   31 seconds ago       Exited (2) 30 seconds ago             app2
419f4defb489   nginx:alpine   "/docker-entrypoint.…"   About a minute ago   Up About a minute           80/tcp    app1
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker stop 9de81346f92e
9de81346f92e
controlplane $ docker rm 9de81346f92e
9de81346f92e
controlplane $ 
controlplane $ 
controlplane $ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
419f4defb489   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   80/tcp    app1
controlplane $ 
controlplane $ 
controlplane $



controlplane $ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
35b5fd281aec   nginx:alpine   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    app2
419f4defb489   nginx:alpine   "/docker-entrypoint.…"   3 minutes ago        Up 3 minutes        80/tcp    app1
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker exec -it 35b5fd281aec sh
/ # 
/ # 
/ # 
/ # ps au
PID   USER     TIME  COMMAND
    1 root      0:00 sleep infinity
    6 root      0:00 sh
   11 root      0:00 ps au
/ # 
/ # 
/ # exit
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker exec -it 419f4defb489 ps aux
PID   USER     TIME  COMMAND
    1 root      0:00 sleep infinity
    6 root      0:00 ps aux
controlplane $ 



### But above gets different pid on kernel however it needs same kernel