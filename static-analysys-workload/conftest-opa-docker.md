controlplane $ cat Dockerfile 
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN go build app.go
CMD ["./app"]
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ cat policy/
base.rego      commands.rego  
controlplane $ cat policy/
base.rego      commands.rego  
controlplane $ cat policy/base.rego 
# from https://www.conftest.dev
package main

denylist = [
  "ubuntu"
]

deny[msg] {
  input[i].Cmd == "from"
  val := input[i].Value
  contains(val[i], denylist[_])

  msg = sprintf("unallowed image found %s", [val])
}
controlplane $ cat policy/commands.rego 
# from https://www.conftest.dev

package commands

denylist = [
  "apk",
  "apt",
  "pip",
  "curl",
  "wget",
]

deny[msg] {
  input[i].Cmd == "run"
  val := input[i].Value
  contains(val[_], denylist[_])

  msg = sprintf("unallowed commands found %s", [val])
}
controlplane $ 





controlplane $ sh run.sh 
FAIL - Dockerfile - main - unallowed image found ["ubuntu"]
FAIL - Dockerfile - commands - unallowed commands found ["apt-get update && apt-get install -y golang-go"]

2 tests, 0 passed, 0 warnings, 2 failures, 0 exceptions
controlplane $ 
controlplane $



# from https://www.conftest.dev

package commands

denylist = [
  "apk",
  "apt",                # remove it
  "pip",
  "curl",
  "wget",
]

deny[msg] {
  input[i].Cmd == "run"
  val := input[i].Value
  contains(val[_], denylist[_])

  msg = sprintf("unallowed commands found %s", [val])
}



controlplane $ sh run.sh 

2 tests, 2 passed, 0 warnings, 0 failures, 0 exceptions
controlplane $ 

