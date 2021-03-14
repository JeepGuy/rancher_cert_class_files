# upgrade rancher commands

### run rke up on AWS 

##### (For some reason you have to be in the correct directory - the same as the cluster config)
#### rke-v1.2.3 up  --disable-port-check   # it doesn't find the  cluster.yml file

#### Attempt 1

- Change the kubernetes_version only , did not erase the system images keyvalue in cluster.yml


rke-v1.2.3 up --config cluster.yml  --disable-port-check


# successful without removing the system_images !!!

#### Attempt 2

Add the internal IP address (to aws)

Backup first 
rke-v1.2.3 etcd snapshot-save \
--config cluster.yml \
--name snapshot-20210118T1100

Mod the cluster.yml file.'

kubernetes_version: "v1.19.4-rancher1-1"

```
nodes:
- address: 34.235.25.20
  port: "22"
  internal_address: ""
  role:
  - controlplane
  - worker
  - etcd
  hostname_override: ""
  user: ubuntu
  docker_socket: /var/run/docker.sock
  ssh_key: ""
  ssh_key_path: ~/.ssh/terraform_id_rsa
  ssh_cert: ""
  ssh_cert_path: ""
  labels: {}
  taints: []
```

```
nodes:
- address: 34.235.25.20
  port: "22"
  internal_address: "172.31.74.29"
  role:
  - controlplane
  - worker
  - etcd
  hostname_override: ""
  user: ubuntu
  docker_socket: /var/run/docker.sock
  ssh_key: ""
  ssh_key_path: ~/.ssh/terraform_id_rsa
  ssh_cert: ""
  ssh_cert_path: ""
  labels: {}
  taints: []
```

rke-v1.2.3 up --config cluster.yml  --disable-port-check

# Add nodes 

create two additional elastic ip addresses in AWS
create two additional nodes in AWS

Launch Instance:

Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-00ddb0e5626798373 
Type: T2 Medium

subnet-087a7f94547666d2a  us-east-1f  

Name Tag: rancher-k8s-cluster-x
wide_open security group

Associate Elastic IP Address

Tips: 

1. Disable swap on workers (nodes) - in cloud environments this should be standard.
        https://kerneltalks.com/howto/5-ways-to-check-swap-on-linux/
            Run cmd:  
            ```cat /proc/swaps```

            STDOUT:
            ```
            Filename				Type		Size	Used	Priority
             - This means there is no swap ...
            ```
2. Check SSH Configuration (on server) (needs ore work)

        - AllowTcpForwarding yes

3. Login to the server.
    
 - Login You will have to have your public key in the authorized_keys file on each host (system) itself.

    if you have ssh keys with a passphrase (as it should)  pass with

        --ssh-agent-auth <passphrase>

i.e.: ssh -i ~/.ssh/terraform_id_rsa ec2-user@107.23.127.222
-  if using ubuntu the user is ubuntu

#### For my instance
ssh -i ~/.ssh/terraform_id_rsa ubuntu@ec2-34-235-25-20.compute-1.amazonaws.com
ssh -i ~/.ssh/terraform_id_rsa ubuntu@34.235.25.20

Assigned Elastic IP address: 34.235.25.20

Public DNS name:   ec2-34-235-25-20.compute-1.amazonaws.com

4. Install Docker

    curl https://releases.rancher.com/install-docker/19.03.sh | sh

5. SSH user in docker group (add)


6. Verify that Docker is owned by ubuntu  (it usually isn't)

    # sudo ls -al /var/run/

    sudo ls -al /var/run/docker #never works on Ubuntu

    sudo chown -R root:ubuntu /var/run/docker
    
```
ubuntu@ip-172-31-66-79:~$ sudo ls -al /var/run/docker
total 0
drwx------  5 root ubuntu 120 Jan 18 16:20 .
drwxr-xr-x 26 root root   960 Jan 18 16:20 ..
drw-------  2 root ubuntu  60 Jan 18 16:20 libnetwork
srwxr-xr-x  1 root ubuntu   0 Jan 18 16:20 metrics.sock
drwx------  2 root ubuntu  40 Jan 18 16:20 plugins
drwx------  2 root ubuntu  40 Jan 18 16:20 swarm
```
    
    #### Docker ownership reverted to root !   NEEDS futher investigations
    
      sudo chown -R ubuntu:ubuntu /var/run/docker

7. Reboot to apply changes

```
 docker ps
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/json: dial unix /var/run/docker.sock: connect: permission denied
```

    sudo systemctl reboot
    
    # sudo systemctl restart docker ###doesn't work.
    
8. Re-login ad verify that docker ps works without sudo.

    docker ps
    
9. Logout and install k8s-rancher

10. Modify the cluster.yml file

11. RKE up command
     rke-v1.2.3 up --config cluster.yml  --disable-port-check

# ERROR

WARN[0140] [etcd] host [34.235.25.20] reported healthy=false 
WARN[0242] [etcd] host [3.217.46.9] failed to check etcd health: failed to get /health for host [3.217.46.9]: Get "https://172.31.66.79:2379/health": Unable to access the service on 172.31.66.79:2379. The service might be still starting up. Error: ssh: rejected: connect failed (Connection refused) 
FATA[0242] Failed to reconcile etcd plane: etcd cluster is unhealthy: hosts [34.235.25.20,3.217.46.9] failed to report healthy. Check etcd container logs on each host for more information 

### Try RKE up again

Failed.

 ##### Remove etcd from the other two nodes.
Removed quotes from internal IP address.
Still failed.

Restore from a snapshop

$ rke etcd snapshot-restore --config cluster.yml --name mysnapshot

rke-v1.2.3 etcd snapshot-restore --config cluster.yml --name snapshot-20210118T1100

--skip-hash-check=false
Closing the issue as it DID WORK as soon as I provided the snapshot name without the .zip extension:

restored from snapshot 
REMOVE the .zip extension from the name of the file.

# add one node at a time. 
# Also Removed the quotes from internal ip adrress in cluster.yml

- address: 52.71.155.59
  port: "22"
  internal_address: 172.31.78.126
  role:
  - controlplane
  - worker
  - etcd
  hostname_override: ""
  user: ubuntu
  docker_socket: /var/run/docker.sock
  ssh_key: ""
  ssh_key_path: ~/.ssh/terraform_id_rsa
  ssh_cert: ""
  ssh_cert_path: ""
  labels: {}
  taints: []







# set kubeconfig
set -x KUBECONFIG (pwd)/kube_config_cluster.yml






# Strange factors 
You have to check the version of hyperkube on dockerhub because rancher renames them without warning.
rke-v1.2.3 config --list-version --all

v1.17.14-rancher1-1
v1.18.12-rancher1-1
v1.19.4-rancher1-1
v1.16.15-rancher1-3

####   rke-v1.2.3 config --version v1.17.14-rancher1-1 

rke-v1.2.3 config --version v1.17.14-rancher1-1 --s    # lists images required  

#### Correct rke up command with the correct version set
rke-v1.2.3 up #  --version v1.17.14-rancher1-linux-amd64

Nope the image must not have been available the first time because the above command with the value set inthe yml file didn't work

rke-v1.2.3 up --config cluster.yml  --disable-port-check

and the version was set in the kubernetes_version in the cluster.yml- instructions vague