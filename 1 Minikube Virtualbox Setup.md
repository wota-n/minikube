# Detailing Steps on Setting Up minikube in Virtual Box on an Arch-based Distro

Writing this down to remember better and as a single source to refer back in the future. Not gonna be entirely accurate because I did not think to document this in the beginning so it is gonna involve a lot of backtracking as I go. More edits will be done whenever needed.

## General issues encountered:
1. minikube cannot start due to Virtualbox settings.
1. Set different drivers for minikube (preferably using Docker - has its own issues that needs to be solved)
1. Some annoyance setting up minikube on an Arch-based distro
1. ??

### Issue 1:

* Enable Nested virtualization

![image](/resources/virtualbox-settings.png)

This should solve most issues even on debian-based distros and others.

### Issue 2:

On arch, install and start docker service with
1. yay -S docker
1. sudo systemctl start docker.service

Current user needs permission to start minikube with docker as the driver. minikube does not allow sudoing this. I believe the command is as below but the error message will print the needed command anyways so just read the error message in case below command does not work.

>sudo usermod -aG docker $USER && newgrp docker

### Issue 3:

Kubectl is not installed together with minikube as a dependency for whatever reason. It is my understanding this issue does not occur in Mac OS according to this [video](https://www.youtube.com/watch?v=E2pP1MOfo3g).

* yay -S kubectl

Running above command should fix this issue easily.

## Change driver

* minikube config set driver docker
* docker can be replaced with virtualbox and other hypervisor software

## Start
Downloads will occur and first time booting takes some time.

* minikube start


## Check Status

* minikube status
* kubectl get nodes



References:

1. https://variable.dk/2017/12/27/minikube-on-ubuntu-in-vmware-nesting-vms/
1. https://minikube.sigs.k8s.io/docs/start/