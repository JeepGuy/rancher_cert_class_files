# Upgrade Rancher the correct way

### There are errors in the Racher docs. This ammends them.

1. Upgrade the local copy of rke - (put the version of rke in the name)

2. Use rke(version) config --list-version -all 
   to see available versions
   
3. Take a one time snapshop of etcd and move that off the cluster host.
     There is no way to rollback an upgrade
     You will have to find a way to restore the cluster from the snapshot
     
4. When the snapshot is complete edit the cluster.yml file 
    Set the kubernetes_version:   "key"
        NOT under the system_images; "key"
           > unless you are using an unsupported k8s version.
           
    *** In new versions (v2.1.5) it appears that htis is set in around line 120 in the kubernetes: key
            and the kubernetes_version: key is blank.
    kubernetes: rancher/hyperkube:v1.19.4-rancher1
    Latest docs as of 01-16-2021 state:
        In case the Kubernetes version is defined in the kubernetes_version directive 
        and under the system-images directive, 
        the system-images configuration will take precedence over the kubernetes_version.
           
5. Then run rke up.          


If you need to change the version of a specific service in the cluster 
   - change that specific value in the cluster.yml file Before you apply the changes. 

