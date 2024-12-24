## FALCO


## vimp - https://falco.org/docs/reference/rules/supported-fields/ - allowed in cks

- falco is Cloud native runtime security

- Access
  - Deep tracing kernel built on linux kernel
  
- Asserting
  - describe security rules against a system
  - detect unwanted behaviour

- Actions
  - Automated response to security violations



## Install Falco on worker node

controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33

node01 $ 
node01 $ 
node01 $ 
node01 $ 
node01 $ curl -s https://falco.org/repo/falcosecurity-packages.asc | apt-key add -
OK
node01 $ echo "deb https://download.falco.org/packages/deb stable main" | tee -a /etc/apt/sources.list.d/falcosecurity.list
deb https://download.falco.org/packages/deb stable main
node01 $ apt-get update -y
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://archive.ubuntu.com/ubuntu focal-updates InRelease [128 kB]                                                                                                                   
Hit:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease                                                                                                                          
Hit:6 http://security.ubuntu.com/ubuntu focal-security InRelease                                          
Get:3 https://d20hasrqv82i0q.cloudfront.net/packages/deb stable InRelease [4168 B]                        
Hit:5 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.31/deb  InRelease
Hit:7 http://ppa.launchpad.net/rmescandon/yq/ubuntu focal InRelease             
Get:8 https://d20hasrqv82i0q.cloudfront.net/packages/deb stable/main amd64 Packages [7166 B]
Fetched 139 kB in 1s (128 kB/s)   
Reading package lists... Done
node01 $ 



node01 $ apt-get install -y falco

node01 $ service falco status
● falco-kmod.service - Falco: Container Native Runtime Security with kmod
     Loaded: loaded (/lib/systemd/system/falco-kmod.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2024-12-17 07:00:25 UTC; 42s ago
       Docs: https://falco.org/docs/
   Main PID: 17904 (falco)
      Tasks: 11 (limit: 2338)
     Memory: 28.5M
     CGroup: /system.slice/falco-kmod.service
             └─17904 /usr/bin/falco -o engine.kind=kmod

Dec 17 07:00:26 node01 falco[17904]:    /etc/falco/falco.yaml | schema validation: ok
Dec 17 07:00:26 node01 falco[17904]: System info: Linux version 5.4.0-131-generic (buildd@lcy02-amd64-108) (gcc version 9.4.0 (Ubuntu 9.4.0-1ubuntu1~20.04.1)) #147-Ubuntu SMP Fri Oct 14 >
Dec 17 07:00:26 node01 falco[17904]: Loading rules from:
Dec 17 07:00:26 node01 falco[17904]:    /etc/falco/falco_rules.yaml | schema validation: ok
Dec 17 07:00:26 node01 falco[17904]:    /etc/falco/falco_rules.local.yaml | schema validation: none
Dec 17 07:00:26 node01 falco[17904]: The chosen syscall buffer dimension is: 8388608 bytes (8 MBs)
Dec 17 07:00:26 node01 falco[17904]: Starting health webserver with threadiness 1, listening on 0.0.0.0:8765
Dec 17 07:00:26 node01 falco[17904]: Loaded event sources: syscall
Dec 17 07:00:26 node01 falco[17904]: Enabled event sources: syscall
Dec 17 07:00:26 node01 falco[17904]: Opening 'syscall' source with Kernel module
lines 1-20/20 (END)

node01 $ 




##### Use falco to find malicious processes inside containers



controlplane $ k run apache --image httpd 
pod/apache created
controlplane $ 
controlplane $ 
controlplane $ k get pod
NAME     READY   STATUS              RESTARTS   AGE
apache   0/1     ContainerCreating   0          3s
controlplane $ k get pod
NAME     READY   STATUS    RESTARTS   AGE
apache   1/1     Running   0          7s
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k exec -it apache -- bash
root@apache:/usr/local/apache2# 



on worker we got log after performing above operation


ode01 $ tail -f /var/log/syslog | grep falco
Dec 17 07:10:43 node01 falco: 07:10:43.393524725: Notice A shell was spawned in a container with an attached terminal (evt_type=execve user=root user_uid=0 user_loginuid=-1 process=bash proc_exepath=/usr/bin/bash parent=runc command=bash terminal=34816 exe_flags=EXE_WRITABLE|EXE_LOWER_LAYER container_id=158af41e7185 container_name=apache)





############################################

## Look at some existing falco rules


## change falco rules

change existing falco rule get custom output format

node01 $ service falco status
● falco.service - Falco: Container Native Runtime Security
     Loaded: loaded (/lib/systemd/system/falco.service; disabled; vendor preset: enabled)
     Active: inactive (dead)
       Docs: https://falco.org/docs/
node01 $ 
node01 $ 
node01 $ 
node01 $ falco
Tue Dec 17 09:15:27 2024: Falco version 0.32.1
Tue Dec 17 09:15:27 2024: Falco initialized with configuration file /etc/falco/falco.yaml
Tue Dec 17 09:15:27 2024: Loading rules from file /etc/falco/falco_rules.yaml:
Tue Dec 17 09:15:27 2024: Loading rules from file /etc/falco/falco_rules.local.yaml:
Tue Dec 17 09:15:28 2024: Starting internal webserver, listening on port 8765

09:16:17.692666735: Warning a shell configuration file has been modified (user=root user_loginuid=-1 command=containerd pcmdline=systemd file=/var/lib/containerd/tmpmounts/containerd-mount3003259083/etc/skel/.bash_logout container_id=host image=<NA>)
09:16:17.692716300: Warning a shell configuration file has been modified (user=root user_loginuid=-1 command=containerd pcmdline=systemd file=/var/lib/containerd/tmpmounts/containerd-mount3003259083/etc/skel/.bashrc container_id=host image=<NA>)
09:16:17.692777707: Warning a shell configuration file has been modified (user=root user_loginuid=-1 command=containerd pcmdline=systemd file=/var/lib/containerd/tmpmounts/containerd-mount3003259083/etc/skel/.profile container_id=host image=<NA>)
09:16:17.694136700: Warning a shell configuration file has been modified (user=root user_loginuid=-1 command=containerd pcmdline=systemd file=/var/lib/containerd/tmpmounts/containerd-mount3003259083/root/.bashrc container_id=host image=<NA>)
09:16:17.694187122: Warning a shell configuration file has been modified (user=root user_loginuid=-1 command=containerd pcmdline=systemd file=/var/lib/containerd/tmpmounts/containerd-mount3003259083/root/.profile container_id=host image=<NA>)
09:16:19.548434255: Warning Log files were tampered (user=root user_loginuid=-1 command=containerd file=/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/66/fs/var/log/dpkg.log container_id=host image=<NA>)
09:16:20.655964403: Warning Log files were tampered (user=root user_loginuid=-1 command=containerd file=/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/67/fs/var/log/dpkg.log container_id=host image=<NA>)
09:16:40.327804809: Notice A shell was spawned in a container with an attached terminal (user=root user_loginuid=-1 apache (id=05a646aa4504) shell=sh parent=runc cmdline=sh terminal=34816 container_id=05a646aa4504 image=docker.io/library/httpd)




^CTue Dec 17 09:17:27 2024: SIGINT received, exiting...
Events detected: 8
Rule counts by severity:
   WARNING: 7
   NOTICE: 1
Triggered rules by rule name:
   Modify Shell Configuration File: 5
   Terminal shell in container: 1
   Clear Log Activities: 2
Syscall event drop monitoring:
   - event drop detected: 0 occurrences
   - num times actions taken: 0
node01 $ 
node01 $ 
node01 $ 
node01 $ cd /etc/falco/      
node01 $ 
node01 $ 
node01 $ grep -r "A shell was spawned in a container with an attached terminal" .
./falco_rules.yaml:    A shell was spawned in a container with an attached terminal (user=%user.name user_loginuid=%user.loginuid %container.info
node01 $ 






node01 $ cat falco_rules.local.yaml
#
# Copyright (C) 2019 The Falco Authors.
#
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

####################
# Your custom rules!
####################

# Add new rules, like this one
# - rule: The program "sudo" is run in a container
#   desc: An event will trigger every time you run sudo in a container
#   condition: evt.type = execve and evt.dir=< and container.id != host and proc.name = sudo
#   output: "Sudo run in container (user=%user.name %container.info parent=%proc.pname cmdline=%proc.cmdline)"
#   priority: ERROR
#   tags: [users, container]

# Or override/append to any rule, macro, or list from the Default Rules

- rule: Terminal shell in container
  desc: A shell was used as the entrypoint/exec point into a container with an attached terminal.
  condition: >
    spawned_process and container
    and shell_procs and proc.tty != 0
    and container_entrypoint
    and not user_expected_terminal_shell_in_container_conditions
  output: >
    %evt.time,user=%user.name,%container.name,%container.id
    shell=%proc.name parent=%proc.pname cmdline=%proc.cmdline terminal=%proc.tty container_id=%container.id image=%container.image.repository)
  priority: WARNING
  tags: [container, shell, mitre_execution]
node01 $ 


