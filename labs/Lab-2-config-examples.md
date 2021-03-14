rke-v1.2.3 config

rancher/hyperkube:v1.19.4-rancher1   # from yaml file.

v1.16.15-rancher1-3
v1.17.14-rancher1-1
v1.19.4-rancher1-1
v1.18.12-rancher1-1

rancher/hyperkube:v1.17.14-rancher1
Docker hub
docker pull rancher/hyperkube:v1.17.14-rancher1-linux-amd64


rancher/hyperkube:v1.17.14-rancher1-linux-amd64






Jamess-MacBook-Pro-3:class_rancher_cert JeepGuy$ rke-v1.2.3 config
[+] Cluster Level SSH Private Key Path [~/.ssh/id_rsa]: ~/.ssh/terraform_id_rsa 	
[+] Number of Hosts [1]: 1
[+] SSH Address of host (1) [none]: 34.235.25.20
[+] SSH Port of host (1) [22]: 22
[+] SSH Private Key Path of host (34.235.25.20) [none]: ~/.ssh/terraform_id_rsa
[+] SSH User of host (34.235.25.20) [ubuntu]: ubuntu
[+] Is host (34.235.25.20) a Control Plane host (y/n)? [y]: y
[+] Is host (34.235.25.20) a Worker host (y/n)? [n]: y
[+] Is host (34.235.25.20) an etcd host (y/n)? [n]: y
[+] Override Hostname of host (34.235.25.20) [none]: ec2-34-235-25-20.compute-1.amazonaws.com
[+] Internal IP of host (34.235.25.20) [none]: 172.31.75.26
[+] Docker socket path on host (34.235.25.20) [/var/run/docker.sock]: 
[+] Network Plugin Type (flannel, calico, weave, canal) [canal]: 
[+] Authentication Strategy [x509]: 
[+] Authorization Mode (rbac, none) [rbac]: 
[+] Kubernetes Docker image [rancher/hyperkube:v1.19.4-rancher1]: rancher/hyperkube:v1.17.14-rancher1-1
[+] Cluster domain [cluster.local]: 
[+] Service Cluster IP Range [10.43.0.0/16]:     
[+] Enable PodSecurityPolicy [n]: 
[+] Cluster Network CIDR [10.42.0.0/16]: 
[+] Cluster DNS Service IP [10.43.0.10]: 
[+] Add addon manifest URLs or YAML files [no]: 


ls -al 
total 96
drwxr-xr-x   9 JeepGuy  staff   288 Jan  1 16:54 .
drwxr-xr-x  16 JeepGuy  staff   512 Jan  1 14:28 ..
-rw-r--r--@  1 JeepGuy  staff  6148 Jan  1 14:15 .DS_Store
-rw-r--r--   1 JeepGuy  staff   119 Jan  1 16:54 .~lock.creating-cluster-config.docx#
-rw-r--r--@  1 JeepGuy  staff  6703 Jan  1 11:01 Preparing Nodes For Kubernetes.docx
drwxr-xr-x  14 JeepGuy  staff   448 Jan  1 14:16 class_files
-rw-r-----   1 JeepGuy  staff  4713 Jan  1 16:53 cluster.yml
-rw-r--r--@  1 JeepGuy  staff  6222 Jan  1 16:54 creating-cluster-config.docx
-rw-r--r--@  1 JeepGuy  staff  8427 Jan  1 16:44 rancher_prep_nodes.docx


ls -al | grep cluster.yml
-rw-r-----   1 JeepGuy  staff  4713 Jan  1 16:53 cluster.yml
Jamess-MacBook-Pro-3:class_rancher_cert JeepGuy$ 


Last login: Fri Jan  1 21:15:05 2021 from 73.133.180.213
ubuntu@ip-172-31-75-26:~$ hostname
ip-172-31-75-26

rke-v1.2.3 config
[+] Cluster Level SSH Private Key Path [~/.ssh/id_rsa]: ~/.ssh/terraform_id_rsa
[+] Number of Hosts [1]: 1
[+] SSH Address of host (1) [none]: 34.235.25.20
[+] SSH Port of host (1) [22]: 
[+] SSH Private Key Path of host (34.235.25.20) [none]: 
[-] You have entered empty SSH key path, trying fetch from SSH key parameter
[+] SSH Private Key of host (34.235.25.20) [none]: ~/.ssh/terraform_id_rsa                    
[+] SSH User of host (34.235.25.20) [ubuntu]: ubuntu
[+] Is host (34.235.25.20) a Control Plane host (y/n)? [y]: y
[+] Is host (34.235.25.20) a Worker host (y/n)? [n]: y
[+] Is host (34.235.25.20) an etcd host (y/n)? [n]: y
[+] Override Hostname of host (34.235.25.20) [none]: 
[+] Internal IP of host (34.235.25.20) [none]: 172.31.75.26
[+] Docker socket path on host (34.235.25.20) [/var/run/docker.sock]: 
[+] Network Plugin Type (flannel, calico, weave, canal) [canal]: 
[+] Authentication Strategy [x509]: 
[+] Authorization Mode (rbac, none) [rbac]: 
[+] Kubernetes Docker image [rancher/hyperkube:v1.19.4-rancher1]: rancher/hyperkube:v1.17.14-rancher1-1
[+] Cluster domain [cluster.local]: 
[+] Service Cluster IP Range [10.43.0.0/16]: 
[+] Enable PodSecurityPolicy [n]: 
[+] Cluster Network CIDR [10.42.0.0/16]: 
[+] Cluster DNS Service IP [10.43.0.10]: 
[+] Add addon manifest URLs or YAML files [no]:






system_images:
  etcd: rancher/coreos-etcd:v3.4.13-rancher1
  alpine: rancher/rke-tools:v0.1.66
  nginx_proxy: rancher/rke-tools:v0.1.66
  cert_downloader: rancher/rke-tools:v0.1.66
  kubernetes_services_sidecar: rancher/rke-tools:v0.1.66
  kubedns: rancher/k8s-dns-kube-dns:1.15.10
  dnsmasq: rancher/k8s-dns-dnsmasq-nanny:1.15.10
  kubedns_sidecar: rancher/k8s-dns-sidecar:1.15.10
  kubedns_autoscaler: rancher/cluster-proportional-autoscaler:1.8.1
  coredns: rancher/coredns-coredns:1.7.0
  coredns_autoscaler: rancher/cluster-proportional-autoscaler:1.8.1
  nodelocal: rancher/k8s-dns-node-cache:1.15.13
  kubernetes: rancher/hyperkube:v1.17.14-rancher1-1
  flannel: rancher/coreos-flannel:v0.13.0-rancher1
  flannel_cni: rancher/flannel-cni:v0.3.0-rancher6
  calico_node: rancher/calico-node:v3.16.1
  calico_cni: rancher/calico-cni:v3.16.1
  calico_controllers: rancher/calico-kube-controllers:v3.16.1
  calico_ctl: rancher/calico-ctl:v3.16.1
  calico_flexvol: rancher/calico-pod2daemon-flexvol:v3.16.1
  canal_node: rancher/calico-node:v3.16.1
  canal_cni: rancher/calico-cni:v3.16.1
  canal_controllers: rancher/calico-kube-controllers:v3.16.1
  canal_flannel: rancher/coreos-flannel:v0.13.0-rancher1
  canal_flexvol: rancher/calico-pod2daemon-flexvol:v3.16.1
  weave_node: weaveworks/weave-kube:2.7.0
  weave_cni: weaveworks/weave-npc:2.7.0
  pod_infra_container: rancher/pause:3.2
  ingress: rancher/nginx-ingress-controller:nginx-0.35.0-rancher2
  ingress_backend: rancher/nginx-ingress-controller-defaultbackend:1.5-rancher1
  metrics_server: rancher/metrics-server:v0.3.6
  windows_pod_infra_container: rancher/kubelet-pause:v0.1.4


