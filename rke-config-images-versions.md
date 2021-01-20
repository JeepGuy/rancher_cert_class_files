


rke-v1.2.3 config --system-images 
INFO[0000] Generating images list for version [v1.19.4-rancher1-1]: 
rancher/coreos-etcd:v3.4.13-rancher1
rancher/rke-tools:v0.1.66
rancher/k8s-dns-kube-dns:1.15.10
rancher/k8s-dns-dnsmasq-nanny:1.15.10
rancher/k8s-dns-sidecar:1.15.10
rancher/cluster-proportional-autoscaler:1.8.1
rancher/coredns-coredns:1.7.0
rancher/k8s-dns-node-cache:1.15.13
rancher/hyperkube:v1.19.4-rancher1
rancher/coreos-flannel:v0.13.0-rancher1
rancher/flannel-cni:v0.3.0-rancher6
rancher/calico-node:v3.16.1
rancher/calico-cni:v3.16.1
rancher/calico-kube-controllers:v3.16.1
rancher/calico-ctl:v3.16.1
rancher/calico-pod2daemon-flexvol:v3.16.1
weaveworks/weave-kube:2.7.0
weaveworks/weave-npc:2.7.0
rancher/pause:3.2
rancher/nginx-ingress-controller:nginx-0.35.0-rancher2
rancher/nginx-ingress-controller-defaultbackend:1.5-rancher1
rancher/metrics-server:v0.3.6



   rke-v1.2.3 config - Setup cluster configuration

USAGE:
   rke-v1.2.3 config [command options] [arguments...]

OPTIONS:
   --name value, -n value  Name of the configuration file (default: "cluster.yml")
   --empty, -e             Generate Empty configuration file
   --print, -p             Print configuration
   --system-images, -s     Generate the default system images
   --list-version, -l      List the default kubernetes version
   --all, -a               Used with -s and -l, get all available versions
   --version value         Generate the default system images for specific k8s versions
   
rke-v1.2.3 config --list-version --all

v1.17.14-rancher1-1
v1.18.12-rancher1-1
v1.19.4-rancher1-1
v1.16.15-rancher1-3

rke-v1.2.3 config --version v1.17.14-rancher1-1 


rke-v1.2.3 config --version v1.17.14-rancher1-1 --s   #(system images flag)

INFO[0000] Generating images list for version [v1.17.14-rancher1-1]: 
rancher/coreos-etcd:v3.4.3-rancher1
rancher/rke-tools:v0.1.66
rancher/k8s-dns-kube-dns:1.15.0
rancher/k8s-dns-dnsmasq-nanny:1.15.0
rancher/k8s-dns-sidecar:1.15.0
rancher/cluster-proportional-autoscaler:1.7.1
rancher/coredns-coredns:1.6.5
rancher/k8s-dns-node-cache:1.15.7
rancher/hyperkube:v1.17.14-rancher1
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



---- from cluster.yml file

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

   
   
