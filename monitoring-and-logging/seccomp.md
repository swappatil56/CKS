

node01 $ docker run nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete 
650ee30bbe5e: Pull complete 
8cc1569e58f5: Pull complete 
362f35df001b: Pull complete 
13e320bf29cd: Pull complete 
7b50399908e1: Pull complete 
57b64962dd94: Pull complete 
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/18 08:44:32 [notice] 1#1: using the "epoll" event method
2024/12/18 08:44:32 [notice] 1#1: nginx/1.27.3
2024/12/18 08:44:32 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/18 08:44:32 [notice] 1#1: OS: Linux 5.4.0-131-generic
2024/12/18 08:44:32 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/18 08:44:32 [notice] 1#1: start worker processes
2024/12/18 08:44:32 [notice] 1#1: start worker process 28
^C2024/12/18 08:44:36 [notice] 1#1: signal 2 (SIGINT) received, exiting
2024/12/18 08:44:36 [notice] 28#28: exiting
2024/12/18 08:44:36 [notice] 28#28: exit
2024/12/18 08:44:36 [notice] 1#1: signal 17 (SIGCHLD) received from 28
2024/12/18 08:44:36 [notice] 1#1: worker process 28 exited with code 0
2024/12/18 08:44:36 [notice] 1#1: exit
node01 $ 
node01 $ 
node01 $ docker run --security-opt seccomp=default.json nginx
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/18 08:45:12 [notice] 1#1: using the "epoll" event method
2024/12/18 08:45:12 [notice] 1#1: nginx/1.27.3
2024/12/18 08:45:12 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/18 08:45:12 [notice] 1#1: OS: Linux 5.4.0-131-generic
2024/12/18 08:45:12 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/18 08:45:12 [notice] 1#1: start worker processes
2024/12/18 08:45:12 [notice] 1#1: start worker process 28
^C2024/12/18 08:45:17 [notice] 1#1: signal 2 (SIGINT) received, exiting
2024/12/18 08:45:17 [notice] 28#28: exiting
2024/12/18 08:45:17 [notice] 28#28: exit
2024/12/18 08:45:17 [notice] 1#1: signal 17 (SIGCHLD) received from 28
2024/12/18 08:45:17 [notice] 1#1: worker process 28 exited with code 0
2024/12/18 08:45:17 [notice] 1#1: exit
node01 $ 



remove write -

node01 $ vi default.json 
node01 $ docker run --security-opt seccomp=default.json nginx
docker: Error response from daemon: OCI runtime start failed: cannot start an already running container: unknown.
node01 $ 
node01 $



## create nginx pod in k8s and assign a seccomp profile to it

