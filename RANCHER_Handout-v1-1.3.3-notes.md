
To upgrade kubernetes

You do this by first upgrading RKE on your host system. 
   Each version of RKE has a specific list of supported Kubernetes versions, 
   which you can find by running 
   
   rke config --list-versions --all.

Back up etcd adnd move off host.

When the snapshot is complete and you know what version you’re upgrading to, 
  edit cluster.yml 


Set that version in the kubernetes_version key.

 In section v1.3.3 - the video different instructions were given.
 It said you have to entire system_images key so it can download the correct images for this kubernetes version.
  
Run rke up, and a short while later your cluster will be upgraded to the new version.
