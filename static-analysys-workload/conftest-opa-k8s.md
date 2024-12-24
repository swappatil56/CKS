############OPA


- opa
- unit test framework
- rego language

Use conftest to check a k8s example against certain rule



controlplane $ git clone git clone https://github.com/killer-sh/cks-course-environment.git
controlplane $ git clone https://github.com/killer-sh/cks-course-environment.git
Cloning into 'cks-course-environment'...
remote: Enumerating objects: 626, done.
remote: Counting objects: 100% (253/253), done.
remote: Compressing objects: 100% (108/108), done.
remote: Total 626 (delta 186), reused 176 (delta 145), pack-reused 373 (from 1)
Receiving objects: 100% (626/626), 168.11 KiB | 4.31 MiB/s, done.
Resolving deltas: 100% (268/268), done.
controlplane $ ls -ltrr
total 12
lrwxrwxrwx 1 root root    1 Dec  6 09:07 filesystem -> /
drwx------ 3 root root 4096 Dec  6 09:12 snap
-rw-r--r-- 1 root root  594 Dec 16 09:04 pod.yaml
drwxr-xr-x 5 root root 4096 Dec 16 09:13 cks-course-environment
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd cks-course-environment/
controlplane $ ls
README.md  Resources.md  Scenarios.md  cluster-setup  course-content
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cd course-content/supply-chain-security/static-analysis/
controlplane $ ls
conftest
controlplane $ cd conftest/
controlplane $ ls
docker  kubernetes
controlplane $ cd kubernetes/
controlplane $ l
deploy.yaml  policy/  run.sh*
controlplane $ cat deploy.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test
  name: test
spec:
  replicas: 1
  selector:
    matchLabels:
      app: test
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test
    spec:
      containers:
        - image: httpd
          name: httpd
          resources: {}
status: {}




controlplane $ vi policy/deployment.rego 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 


controlplane $ cat policy/deployment.rego 



# from https://www.conftest.dev
package main

deny[msg] {
  input.kind = "Deployment"
  not input.spec.template.spec.securityContext.runAsNonRoot = true
  msg = "Containers must not run as root"
}

deny[msg] {
  input.kind = "Deployment"
  not input.spec.selector.matchLabels.app
  msg = "Containers must provide app label for pod selectors"
}



controlplane $ cat run.sh 
docker run --rm -v $(pwd):/project openpolicyagent/conftest test deploy.yaml
controlplane $ 




controlplane $ docker run --rm -v $(pwd):/project openpolicyagent/conftest test deploy.yaml
Unable to find image 'openpolicyagent/conftest:latest' locally
latest: Pulling from openpolicyagent/conftest
43c4264eed91: Pull complete 
ed52fa1ceb1a: Pull complete 
57f0782758f1: Pull complete 
fc561b8113b8: Pull complete 
f191b835b54c: Pull complete 
Digest: sha256:6ddf5173e09839f9c6850f51593e9b840ec3f709c808c37433cf5f20d58fb2b0
Status: Downloaded newer image for openpolicyagent/conftest:latest
FAIL - deploy.yaml - main - Containers must not run as root

2 tests, 1 passed, 0 warnings, 1 failure, 0 exceptions
controlplane $ vi deploy.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi deploy.yaml 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ docker run --rm -v $(pwd):/project openpolicyagent/conftest test deploy.yaml
FAIL - deploy.yaml - main - Containers must not run as root

2 tests, 1 passed, 0 warnings, 1 failure, 0 exceptions
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ vi deploy.yaml 
controlplane $ docker run --rm -v $(pwd):/project openpolicyagent/conftest test deploy.yaml

2 tests, 2 passed, 0 warnings, 0 failures, 0 exceptions
controlplane $ 
controlplane $ 



controlplane $ cat deploy.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test
  name: test
spec:
  replicas: 1
  selector:
    matchLabels:
      app: test
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test
    spec:
      securityContext:
         runAsNonRoot: true
      containers:
        - image: httpd
          name: httpd
          resources: {}
status: {}