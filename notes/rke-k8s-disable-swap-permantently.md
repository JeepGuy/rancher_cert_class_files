# Permanently Disable Swap for Kubernetes Cluster
Retrieved from https://brandonwillmott.com/2020/10/15/permanently-disable-swap-for-kubernetes-cluster/      on 01 Jan 2021

I set up a few Kubernetes clusters preparing for the CKA exam and discovered that upon reboot, y control plane node didn’t work. Running any kubectl command I get:
The connection to the server 192.168.1.57:6443 was refused - did you specify the right host or port?
This is a common error message that can result from numerous issues but I started troubleshooting by seeing if the kubelet process was running with ps aux | grep kube. Nothing…no kubelet service running. Then I looked at /var/log/syslog and I found the problem — swap was back on!
Oct 15 06:23:13 master-02 kubelet[4657]: F1015 06:23:13.446790 4657 server.go:265] failed to run Kubelet: running with swap on is not supported, please disable swap! or set --fail-swap-on flag to false. /proc/swaps contained: [Filename#011#011#011#011Type#011#011Size#011Used#011Priority /dev/dm-1 partition#0112097148#0110#011-2]
It turns out even though I turned the swap off with swapoff -a, that’s only a temporary solution for disabling the swap. Upon reboot, it will be enabled due to it being referenced in /etc/fstab:
/dev/mapper/ubuntu--vg-swap_1 none swap sw 0 0
To disable permanently, you can run the following command:
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
This command will insert a comment on the line referencing swap in /etc/fstab but will not take effect immediately so a reboot will be necessary. If you want to avoid a reboot, you can also run sudo swapoff -a again and wait for the kubelet process to retry again or force the service to restart with sudo systemctl restart kubelet.
The topic of Kubernetes not supporting linux memory management techniques like paging to disk has puzzled many people and there’s a good discussion about it in a GitHub issue that was raised: Kubelet/Kubernetes should work with Swap Enabled. Suffice to say, swap support isn’t changing anytime soon.


# Also retreived from internet on 1 Jan 2021
https://platform9.com/blog/support/disabling-swap-kubernetes-node/

Run the following command to disable swap immediately.
 sudo swapoff -a 
Run the following command to update fstab so that swap remains disabled after a reboot.
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab