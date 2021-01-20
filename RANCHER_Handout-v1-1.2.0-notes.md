#### RANCHER_Handout-v1-1.2.0-notes.md

# Discovering RKE
Unit 1.2


## Introduction
There are two ways to install Rancher - a standalone way that’s good for sandbox environments, and another way that deploys Rancher into a highly available Kubernetes cluster. 
     For that cluster we use the Rancher Kubernetes Engine, also known as RKE.
     
RKE is 100% upstream Kubernetes, certified by the Cloud Native Computing Foundation. The only change that we make to it is that it runs entirely in Docker containers. 

This makes it extremely portable and quick to deploy - you don't need anything else on the host other than a supported version of Docker.

RKE uses a declarative configuration to define the cluster, so after entering the hosts and their roles, you run rke up to provision the cluster.

The RKE binary runs from your local workstation or a shared management host, not from the cluster nodes themselves. 

It connects to the nodes over SSH, 
installs Kubernetes and 
wires the nodes together, 
and then returns a config that you use with kubectl to access the cluster.

When you need to make changes to the cluster, like when you upgrade Kubernetes, you change the config file and then run rke up again to apply those changes.

Because everything runs in Docker containers, upgrades are easy and safe.

#### References:
Overview of RKE - https://rancher.com/docs/rke/latest/en/