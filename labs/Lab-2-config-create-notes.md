rke-config-create.md

You have to check the version of hyperkube on dockerhub because rancher renames them without warning.
rke-v1.2.3 config --list-version --all

v1.17.14-rancher1-1
v1.18.12-rancher1-1
v1.19.4-rancher1-1
v1.16.15-rancher1-3

rke-v1.2.3 config --version v1.17.14-rancher1-1

rancher/hyperkube:v1.17.14-rancher1-linux-amd64  # is the image it downloaded. 


rke-v1.2.3 config --version v1.17.14-rancher1-1 --s   WRONG  

It is actually:

rke-v1.2.3 up --version v1.17.14-rancher1-linux-amd64
