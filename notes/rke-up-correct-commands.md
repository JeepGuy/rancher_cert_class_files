# run rke up on AWS 

# (For some reason you have to be inthe correct directory - the same as the cluster config)

rke-v1.2.3 up --config cluster.yml  --disable-port-check

rke-v1.2.3 up  --disable-port-check

You have to check the version of hyperkube on dockerhub because rancher renames them without warning.
rke-v1.2.3 config --list-version --all

v1.17.14-rancher1-1
v1.18.12-rancher1-1
v1.19.4-rancher1-1
v1.16.15-rancher1-3

####   rke-v1.2.3 config --version v1.17.14-rancher1-1 

rke-v1.2.3 config --version v1.17.14-rancher1-1 --s   

#### Correct rke up command with the correct version set
rke-v1.2.3 up #  --version v1.17.14-rancher1-linux-amd64

Nope the image must not ahve been available because the above command didn't work

rke-v1.2.3 up --config cluster.yml  --disable-port-check

and the version was set in the kubernetes_version in the cluster.yml- instructions vague


####  rke-v1.2.3 config --version v1.17.14-rancher1-1 --s

INFO[0000] Generating images list for version [v1.17.14-rancher1-1]: 
rancher/coreos-etcd:v3.4.3-rancher1
rancher/rke-tools:v0.1.66
rancher/k8s-dns-kube-dns:1.15.0
rancher/k8s-dns-dnsmasq-nanny:1.15.0
rancher/k8s-dns-sidecar:1.15.0
rancher/cluster-proportional-autoscaler:1.7.1
rancher/coredns-coredns:1.6.5
rancher/k8s-dns-node-cache:1.15.7
rancher/hyperkube:v1.17.14-rancher1   ### this is not longer on dockerhub that is why it fails.
rancher/coreos-flannel:v0.12.0
rancher/flannel-cni:v0.3.0-rancher6
rancher/calico-node:v3.13.4
rancher/calico-cni:v3.13.4
rancher/calico-kube-controllers:v3.13.4
rancher/calico-ctl:v3.13.4
rancher/calico-pod2daemon-flexvol:v3.13.4
weaveworks/weave-kube:2.6.4
weaveworks/weave-npc:2.6.4
rancher/pause:3.1
rancher/nginx-ingress-controller:nginx-0.35.0-rancher2
rancher/nginx-ingress-controller-defaultbackend:1.5-rancher1
rancher/metrics-server:v0.3.6


# Cannot downgrade...
Jamess-MacBook-Pro-9:rke_configs JeepGuy$ rke-v1.2.3 up --config cluster.yml
INFO[0000] Running RKE version: v1.2.3                  
INFO[0000] Initiating Kubernetes cluster                
FATA[0000] Failed to validate cluster: v1.17.14-rancher1-linux-amd64 is an unsupported Kubernetes version and system images are not populated: etcd image is not populated


Jamess-MacBook-Pro-9:rke_configs JeepGuy$ rke-v1.2.3 up --config cluster.yml
INFO[0000] Running RKE version: v1.2.3                  
INFO[0000] Initiating Kubernetes cluster                
FATA[0000] Failed to validate cluster: v1.17.14-rancher1 is an unsupported Kubernetes version and system images are not populated: etcd image is not populated 

INFO[0083] [healthcheck] Start Healthcheck on service [kubelet] on host [34.235.25.20] 
ERRO[0141] Failed to upgrade hosts: 34.235.25.20 with error [Failed to verify healthcheck: Failed to check http://localhost:10248/healthz for service [kubelet] on host [34.235.25.20]: Get "http://localhost:10248/healthz": Unable to access the service on localhost:10248. The service might be still starting up. Error: ssh: rejected: connect failed (Connection refused), log: Please drain this node and delete the CPU manager checkpoint file "/var/lib/kubelet/cpu_manager_state" before restarting Kubelet.] 
FATA[0141] [controlPlane] Failed to upgrade Control Plane: [[Failed to verify healthcheck: Failed to check http://localhost:10248/healthz for service [kubelet] on host [34.235.25.20]: Get "http://localhost:10248/healthz": Unable to access the service on localhost:10248. The service might be still starting up. Error: ssh: rejected: connect failed (Connection refused), log: Please drain this node and delete the CPU manager checkpoint file "/var/lib/kubelet/cpu_manager_state" before restarting Kubelet.]]

### try with disable port check

rke-v1.2.3 up --config cluster.yml  --disable-port-check


ERRO[0108] Failed to upgrade worker components on NotReady hosts, error: [Failed to verify healthcheck: Failed to check http://localhost:10248/healthz for service [kubelet] on host [34.235.25.20]: Get "http://localhost:10248/healthz": Unable to access the service on localhost:10248. The service might be still starting up. Error: ssh: rejected: connect failed (Connection refused), log: Please drain this node and delete the CPU manager checkpoint file "/var/lib/kubelet/cpu_manager_state" before restarting Kubelet.] 
INFO[0108] [controlplane] Now checking status of node 34.235.25.20, try #1 
INFO[0113] [controlplane] Now checking status of node 34.235.25.20, try #2 
INFO[0118] [controlplane] Now checking status of node 34.235.25.20, try #3 
INFO[0123] [controlplane] Now checking status of node 34.235.25.20, try #4 
INFO[0128] [controlplane] Now checking status of node 34.235.25.20, try #5 
ERRO[0133] Host 34.235.25.20 failed to report Ready status with error: host 34.235.25.20 not ready 
INFO[0133] [controlplane] Processing controlplane hosts for upgrade 1 at a time 
INFO[0133] Processing controlplane host 34.235.25.20    
INFO[0133] [controlplane] Now checking status of node 34.235.25.20, try #1 
INFO[0138] [controlplane] Now checking status of node 34.235.25.20, try #2 
INFO[0144] [controlplane] Now checking status of node 34.235.25.20, try #3 
INFO[0149] [controlplane] Now checking status of node 34.235.25.20, try #4 
INFO[0154] [controlplane] Now checking status of node 34.235.25.20, try #5 
ERRO[0159] Failed to upgrade hosts: 34.235.25.20 with error [host 34.235.25.20 not ready] 
FATA[0159] [controlPlane] Failed to upgrade Control Plane: [[host 34.235.25.20 not ready]] 
  ### next attempt:
  
  (Connection refused), log: Please drain this node and delete the CPU manager checkpoint file "/var/lib/kubelet/cpu_manager_state" before restarting Kubelet.] 
  
ubuntu@ip-172-31-74-29:~$ ls -al /var/lib/kubelet/cpu_manager_state
-rw------- 1 root root 62 Jan 12 01:19 /var/lib/kubelet/cpu_manager_state
ubuntu@ip-172-31-74-29:~$ cat  /var/lib/kubelet/cpu_manager_state
cat: /var/lib/kubelet/cpu_manager_state: Permission denied
ubuntu@ip-172-31-74-29:~$ sudo cat  /var/lib/kubelet/cpu_manager_state
{"policyName":"none","defaultCpuSet":"","checksum":1353318690}ubuntu@ip-172-31-74-29:~$

### Downgrade worked !!!

INFO[0046] Finished building Kubernetes cluster successfully

# fix

https://forums.rancher.com/t/cant-access-kubeapi-port-6443-when-rke-up-on-aws/16530/2

References: https://github.com/rancher/rke/issues/1256

Jun '20
I’ve found the solution on github: https://github.com/rancher/rke/issues/1256 19
RKE should perform preliminary KubeAPI port check over HTTP - not raw TCP


Basically use the option

--disable-port-check
example:

rke up --disable-port-check





~/.ssh/terraform_id_rsa