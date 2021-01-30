# kubernetes-playbook

Playbook to create a Kubernetes cluster using kubeadm with n number nodes.

[![ansible-lint Actions Status](https://github.com/NilsCarstensen/kubernetes-ansible-playbook/workflows/ansible-lint/badge.svg)](https://github.com/NilsCarstensen/kubernetes-ansible-playbook/actions)

## What is this playbook doing?

1. Creating Kubernetes user and group and assing wheel group.
2. Setting up required networking settings.
3. Adding docker repositories and install docker-ce, docker-ce-cli, and containerd.
4. Setting up docker daemon.
5. Adding Kubernetes repositories and install kubelet, kubectl, and kubeadm.
6. Installation gets split off based on the hosts Kubernetes role e.g (master or worker).  
6.1 Master:  
    1. Configure firewall
    2. check if cluster is already initialized
    3. create new cluster
    4. enable kubectl for kubernetes user    
6.2 Worker:
    1. Configure firewall
    2. Run cluster join command

## When should you use this playbook? 
You should use this playbook if you need a basic yet fast installation of your own Kubernetes cluster.   
The playbook itself takes care of your container runtime, firewall rules, required networking, and installation of required packages (and repository) in order to run a Kubernetes cluster.

The best purpose of using this playbook is when you start learning Kubernetes and need an environment to use as a lab.

All tasks inside this playbook are based on the installation instructions that can be found in the official Kubernetes documentation.


## Setup inventory file:

    [kubernetes_masters]
    IP address of your master node.


    [kubernetes_nodes]
    List of IP addresses of your worker nodes.

## Assign variables:

Assign the variables "node" and "master" based on the role you want them to execute.
A very basic site.yml file could look like this.


    ---
      - hosts: kubernetes_masters
        become: true
        vars:
          kubernetes_role: master
        roles:
          - kubernetes-playbook

      - hosts: kubernetes_nodes
        become: true
        vars:
          kubernetes_role: node
        roles:
          - kubernetes-playbook
