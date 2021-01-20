# Rancher Node Preparation    unit 1.2.2

Rancher has docker installation scripts for your chosen flavor of Linux

For AWS:

Launch Instance:

Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-00ddb0e5626798373 
Type: T2 Medium
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
2. Check SSH Configuration (on server)

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

  sudo usermod -aG docker ubuntu


6. Verify that Docker is owned by ubuntu  (it usually isn't)

    sudo ls -al /var/run/

    sudo ls -al /var/run/docker

    sudo chown -R root:ubuntu /var/run/docker
    
    #### Docker ownership reverted to root !   NEEDS futher investigations
    
      sudo chown -R ubuntu:ubuntu /var/run/docker

7. Reboot to apply changes

    sudo systemctl reboot
    
8. Re-login ad verify that docker ps works without sudo.

    docker ps
    
9. Logout and install k8s-rancher


