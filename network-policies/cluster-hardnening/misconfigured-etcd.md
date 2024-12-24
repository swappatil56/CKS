Misconfigure ETCD connection
Change the existing Apiserver manifest argument to: --etcd-servers=this-is-very-wrong .

Check what the logs say, without using anything in /var .

Fix the Apiserver again.


Log Locations

Log locations to check:

/var/log/pods
/var/log/containers
crictl ps + crictl logs
docker ps + docker logs (in case when Docker is used)
kubelet logs: /var/log/syslog or journalctl



controlplane $ vi /etc/kubernetes/manifests/kube-apiserver.yaml 
controlplane $ 
controlplane $ 
controlplane $ cd /var/log/syslog
bash: cd: /var/log/syslog: Not a directory
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ tail /var/log/syslog
Dec 12 05:20:10 controlplane containerd[653]: time="2024-12-12T05:20:10.524841916Z" level=info msg="RemoveContainer for \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\""
Dec 12 05:20:10 controlplane kubelet[707]: I1212 05:20:10.525597     707 status_manager.go:851] "Failed to get status for pod" podUID="0cfa7f19a2c8cf4c1add14122593c823" pod="kube-system/kube-scheduler-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-scheduler-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:20:10 controlplane kubelet[707]: I1212 05:20:10.526022     707 status_manager.go:851] "Failed to get status for pod" podUID="0cfa7f19a2c8cf4c1add14122593c823" pod="kube-system/kube-scheduler-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-scheduler-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:20:10 controlplane kubelet[707]: I1212 05:20:10.526274     707 status_manager.go:851] "Failed to get status for pod" podUID="53ebb29699412c968f4d993ced098d57" pod="kube-system/kube-apiserver-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-apiserver-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:20:10 controlplane kubelet[707]: I1212 05:20:10.526457     707 status_manager.go:851] "Failed to get status for pod" podUID="a55d9c391dc5f492555b54cdef44652d" pod="kube-system/kube-controller-manager-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-controller-manager-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:20:10 controlplane containerd[653]: time="2024-12-12T05:20:10.564724092Z" level=info msg="RemoveContainer for \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\" returns successfully"
Dec 12 05:20:10 controlplane kubelet[707]: I1212 05:20:10.567665     707 scope.go:117] "RemoveContainer" containerID="9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a"
Dec 12 05:20:10 controlplane containerd[653]: time="2024-12-12T05:20:10.568113807Z" level=error msg="ContainerStatus for \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\" failed" error="rpc error: code = NotFound desc = an error occurred when try to find container \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\": not found"
Dec 12 05:20:10 controlplane kubelet[707]: E1212 05:20:10.568360     707 log.go:32] "ContainerStatus from runtime service failed" err="rpc error: code = NotFound desc = an error occurred when try to find container \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\": not found" containerID="9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a"
Dec 12 05:20:10 controlplane kubelet[707]: I1212 05:20:10.568462     707 pod_container_deletor.go:53] "DeleteContainer returned error" containerID={"Type":"containerd","ID":"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a"} err="failed to get container status \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\": rpc error: code = NotFound desc = an error occurred when try to find container \"9e7162548bc9b646a449ff7b7864685ef349dbf156f3e5ca1f0d1cdeeb521a4a\": not found"
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ 
controlplane $ k get pod -n kube-system
Get "https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods?limit=500": dial tcp 172.30.1.2:6443: connect: connection refused - error from a previous attempt: read tcp 172.30.1.2:39762->172.30.1.2:6443: read: connection reset by peer
controlplane $ 
controlplane $ 




# 1) if we would check the /var directory
cat /var/log/pods/kube-system_kube-apiserver-controlplane_e24b3821e9bdc47a91209bfb04056993/kube-apiserver/X.log
> Err: connection error: desc = "transport: Error while dialing dial tcp: address this-is-very-wrong: missing port in address". Reconnecting...

# 2) but here we want to find other ways, so we check the container logs
crictl ps # maybe run a few times, because the apiserver container get's restarted
crictl logs f669a6f3afda2
> Error while dialing dial tcp: address this-is-very-wrong: missing port in address. Reconnecting...


controlplane $ crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
a1aeb54835ec2       604f5db92eaa8       8 seconds ago       Running             kube-apiserver            4                   f9570d4849977       kube-apiserver-controlplane
0963edc90a57d       f9c3c1813269c       51 seconds ago      Running             calico-kube-controllers   3                   d82497844b784       calico-kube-controllers-94fb6bc47-5w8sl
70d7d18013b5c       045733566833c       3 minutes ago       Running             kube-controller-manager   4                   8e2efe0bbf448       kube-controller-manager-controlplane
5879a7aa19734       1766f54c897f0       3 minutes ago       Running             kube-scheduler            4                   272f52cd11544       kube-scheduler-controlplane
c211ffbef5972       95fef08b8bf89       44 minutes ago      Running             local-path-provisioner    1                   f97d6c2b1d29d       local-path-provisioner-6c5cff8948-phnkg
fecf83dea1a6e       cbb01a7bd410d       44 minutes ago      Running             coredns                   1                   bbcacc6067456       coredns-57888bfdc7-j9ddk
35cbf4e4a7e83       cbb01a7bd410d       44 minutes ago      Running             coredns                   1                   f50472b4472f4       coredns-57888bfdc7-p24nh
199890e89dd69       e6ea68648f0cd       44 minutes ago      Running             kube-flannel              1                   e2f54d7c62a37       canal-cdcf7
6b3496a62e832       75392e3500e36       44 minutes ago      Running             calico-node               1                   e2f54d7c62a37       canal-cdcf7
f33dbb6c6fb0a       ad83b2ca7b09e       44 minutes ago      Running             kube-proxy                1                   f24c6743fef02       kube-proxy-bt2pv
6beddd9b16bfe       2e96e5913fc06       45 minutes ago      Running             etcd                      1                   52793f5554449       etcd-controlplane
controlplane $ crictl logs a1aeb54835ec2
I1212 05:23:29.609065       1 options.go:228] external host was not specified, using 172.30.1.2
I1212 05:23:29.610463       1 server.go:142] Version: v1.31.0
I1212 05:23:29.610604       1 server.go:144] "Golang settings" GOGC="" GOMAXPROCS="" GOTRACEBACK=""
I1212 05:23:30.057756       1 plugins.go:157] Loaded 12 mutating admission controller(s) successfully in the following order: NamespaceLifecycle,LimitRanger,ServiceAccount,NodeRestriction,TaintNodesByCondition,Priority,DefaultTolerationSeconds,DefaultStorageClass,StorageObjectInUseProtection,RuntimeClass,DefaultIngressClass,MutatingAdmissionWebhook.
I1212 05:23:30.057924       1 plugins.go:160] Loaded 13 validating admission controller(s) successfully in the following order: LimitRanger,ServiceAccount,PodSecurity,Priority,PersistentVolumeClaimResize,RuntimeClass,CertificateApproval,CertificateSigning,ClusterTrustBundleAttest,CertificateSubjectRestriction,ValidatingAdmissionPolicy,ValidatingAdmissionWebhook,ResourceQuota.
I1212 05:23:30.058217       1 instance.go:232] Using reconciler: lease
I1212 05:23:30.062929       1 shared_informer.go:313] Waiting for caches to sync for node_authorizer
I1212 05:23:30.063415       1 shared_informer.go:313] Waiting for caches to sync for *generic.policySource[*k8s.io/api/admissionregistration/v1.ValidatingAdmissionPolicy,*k8s.io/api/admissionregistration/v1.ValidatingAdmissionPolicyBinding,k8s.io/apiserver/pkg/admission/plugin/policy/validating.Validator]
W1212 05:23:30.063667       1 logging.go:55] [core] [Channel #1 SubChannel #4]grpc: addrConn.createTransport failed to connect to {Addr: "this-is-very-wrong", ServerName: "this-is-very-wrong", }. Err: connection error: desc = "transport: Error while dialing: dial tcp: address this-is-very-wrong: missing port in address"
W1212 05:23:30.063784       1 logging.go:55] [core] [Channel #2 SubChannel #5]grpc: addrConn.createTransport failed to connect to {Addr: "this-is-very-wrong", ServerName: "this-is-very-wrong", }. Err: connection error: desc = "transport: Error while dialing: dial tcp: address this-is-very-wrong: missing port in address"
W1212 05:23:30.063902       1 logging.go:55] [core] [Channel #3 SubChannel #6]grpc: addrConn.createTransport failed to connect to {Addr: "this-is-very-wrong", ServerName: 
controlplane $ 





# 3) what about syslogs
journalctl | grep apiserver # nothing specific
cat /var/log/syslog | grep apiserver # nothing specific


controlplane $ tail /var/log/syslog | grep api
Dec 12 05:26:20 controlplane kubelet[707]: I1212 05:26:20.289771     707 kubelet.go:1895] "Trying to delete pod" pod="kube-system/kube-apiserver-controlplane" podUID="c2a929a7-3bbe-41b0-8d43-d8ee5af1e08b"
Dec 12 05:26:20 controlplane kubelet[707]: E1212 05:26:20.290581     707 mirror_client.go:138] "Failed deleting a mirror pod" err="Delete \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-apiserver-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused" pod="kube-system/kube-apiserver-controlplane"
Dec 12 05:26:20 controlplane kubelet[707]: E1212 05:26:20.291853     707 pod_workers.go:1301] "Error syncing pod, skipping" err="failed to \"StartContainer\" for \"kube-apiserver\" with CrashLoopBackOff: \"back-off 2m40s restarting failed container=kube-apiserver pod=kube-apiserver-controlplane_kube-system(18eff41e0a55d055afc8daff0a02aff3)\"" pod="kube-system/kube-apiserver-controlplane" podUID="18eff41e0a55d055afc8daff0a02aff3"
Dec 12 05:26:21 controlplane kubelet[707]: E1212 05:26:21.114086     707 controller.go:145] "Failed to ensure lease exists, will retry" err="Get \"https://172.30.1.2:6443/apis/coordination.k8s.io/v1/namespaces/kube-node-lease/leases/controlplane?timeout=10s\": dial tcp 172.30.1.2:6443: connect: connection refused" interval="7s"
Dec 12 05:26:21 controlplane kubelet[707]: E1212 05:26:21.902463     707 event.go:368] "Unable to write event (may retry after sleeping)" err="Patch \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/events/kube-controller-manager-controlplane.1810561a2d4787d5\": dial tcp 172.30.1.2:6443: connect: connection refused" event="&Event{ObjectMeta:{kube-controller-manager-controlplane.1810561a2d4787d5  kube-system   4012 0 0001-01-01 00:00:00 +0000 UTC <nil> <nil> map[] map[] [] [] []},InvolvedObject:ObjectReference{Kind:Pod,Namespace:kube-system,Name:kube-controller-manager-controlplane,UID:a55d9c391dc5f492555b54cdef44652d,APIVersion:v1,ResourceVersion:,FieldPath:spec.containers{kube-controller-manager},},Reason:BackOff,Message:Back-off restarting failed container kube-controller-manager in pod kube-controller-manager-controlplane_kube-system(a55d9c391dc5f492555b54cdef44652d),Source:EventSource{Component:kubelet,Host:controlplane,},FirstTimestamp:2024-12-12 05:15:26 +0000 UTC,LastTimestamp:2024-12-12 05:19:52.486410913 +0000 UTC m=+2482.584547393,Count:5,Type:Warning,EventTime:0001-01-01 00:00:00 +0000 UTC,Series:nil,Action:,Related:nil,ReportingController:kubelet,ReportingInstance:controlplane,}"
Dec 12 05:26:24 controlplane kubelet[707]: I1212 05:26:24.290698     707 status_manager.go:851] "Failed to get status for pod" podUID="0cfa7f19a2c8cf4c1add14122593c823" pod="kube-system/kube-scheduler-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-scheduler-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:26:24 controlplane kubelet[707]: I1212 05:26:24.292200     707 status_manager.go:851] "Failed to get status for pod" podUID="e8e80d21-0469-4494-a5db-5c4c1d214f3d" pod="kube-system/calico-kube-controllers-94fb6bc47-5w8sl" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/calico-kube-controllers-94fb6bc47-5w8sl\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:26:24 controlplane kubelet[707]: I1212 05:26:24.292757     707 status_manager.go:851] "Failed to get status for pod" podUID="18eff41e0a55d055afc8daff0a02aff3" pod="kube-system/kube-apiserver-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-apiserver-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
Dec 12 05:26:24 controlplane kubelet[707]: I1212 05:26:24.293055     707 status_manager.go:851] "Failed to get status for pod" podUID="a55d9c391dc5f492555b54cdef44652d" pod="kube-system/kube-controller-manager-controlplane" err="Get \"https://172.30.1.2:6443/api/v1/namespaces/kube-system/pods/kube-controller-manager-controlplane\": dial tcp 172.30.1.2:6443: connect: connection refused"
controlplane $ 




