

Preparing Nodes For Kubernetes
Unit 1.2.2


Docker
Prepare Linux nodes via whatever means you want. You can provision them manually, with Ansible, Terraform, Puppet, Chef, cloud-init, shell scripts, or anything else. As a final step, install Docker onto them.
But not just any version of Docker.
Kubernetes has a list of supported Docker versions available in their docs.
Most Linux flavors are suitable for deploying RKE out of the box, but make sure that:
• The SSH user is in the Docker group
• Swap is disabled on any worker nodes (this is the default in proper cloud environments)
If you're using the RHEL/CentOS version of Docker, you'll have to make additional changes that are covered in our documentation.
To make the installation easier for you, Rancher has versioned installation scripts that will deploy the correct version of Docker for your chosen Linux flavor.
Ports
Your environment might have security policies that limit network traffic. Traffic from the node where you're running RKE needs to be able to reach port 22 on every Kubernetes node and also 6443 on every control plane node. That's the port for the Kubernetes API.
For the cluster itself, there's a page in our documentation that covers which ports need to be open to where. This level of port configuration is not required - it depends on your security posture. Development or lab environments in secure locations might simply open up all

communication between all nodes in the cluster and restrict access to those nodes from outside of the cluster subnet.
References
Supported Versions of Docker in Kubernetes - https://kubernetes.io/docs/setup/production-environment/container-runtimes/#docker
RHEL/CentOS Docker Information - https://rancher.com/docs/rke/latest/en/os/#using-rhel-centos-packaged-docker
Versioned Docker Installation Scripts From Rancher - https://rancher.com/docs/rancher/v2.x/en/installation/requirements/installing-docker/
RKE Port Configuration - https://rancher.com/docs/rke/latest/en/os/#ports