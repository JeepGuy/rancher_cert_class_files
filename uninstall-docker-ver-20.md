# rancher unistall docker version 20

https://stackoverflow.com/questions/31313497/how-to-remove-docker-installed-using-wget?answertab=active#tab-top

The uninstallation step mentions:

sudo apt-get purge -y docker-engine
sudo apt-get autoremove -y --purge docker-engine
sudo apt-get autoclean
Note: chasmani adds in the comments:

I had to also add docker-ce, docker.io and docker to the first two lines to completely get rid of
sudo apt-get purge -y docker-engine docker docker.io docker-ce
sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce
It adds:

The above commands will not remove images, containers, volumes, or user created configuration files on your host. If you wish to delete all images, containers, and volumes run the following command:
sudo rm -rf /var/lib/docker
Remove docker from apparmor.d:
sudo rm /etc/apparmor.d/docker
Remove docker group:
sudo groupdel docker
As Micah Smith adds in the comments:

You may (as I did) also need to remove runtime files such as /var/run/docker.sock.
Try find / -name '*docker*' to see all of these files. (This searches your entire filesystem, look in at least /var, /run, /etc separately if you prefer not to do this.)
Now, You have successfully deleted docker.




## Failed attempts
sudo apt-get remove docker docker-engine docker.io containerd runc

ubuntu@ip-172-31-75-26:~$ sudo apt-get remove docker docker-engine docker.io containerd runc
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package 'docker-engine' is not installed, so not removed
Package 'containerd' is not installed, so not removed
Package 'runc' is not installed, so not removed
Package 'docker' is not installed, so not removed
Package 'docker.io' is not installed, so not removed
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

didn't work.

docker --version
Docker version 20.10.1, build 831ebea

# Also didn't work.

sudo apt-get purge -y docker.io 

sudo apt-get autoremove -y --purge docker.io

sudo apt-get autoclean

sudo rm -rf /var/lib/docker

sudo rm -rf /etc/docker

sudo rm /etc/apparmor.d/docker

sudo apt-get purge runc containerd docker.io