[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
# Ansible Bare Metal Kubernetes Cluster
This role installs Kubernetes with kubeadm on your hosts. You can provide as many nodes as you want. Currently, you can choose one of the three main container runtimes, see the "variables" section for more information. Make sure you use the appropriate runtime version regarding the Kubernetes version you want to deploy. You can specify versions for kubelet, kubectl, kubeadm, keep in mind it's highly recommended to run the same version on each one of these.

&nbsp;
# Getting started
Start by setting the kubernetes_role= 'master' variable on your Kubernetes masters. Set kubernets_role= 'node' on your Kubernetes nodes. Furthermore you need to specify the container runtime and it's version. After that you need to set the value for all Kubernetes component versions.

Check the defaults, maybe it fits your needs, so you don't need to set every variable.

&nbsp;
# Variables
| Variable               |  Default                      | Description                                       |
| :----------------------| :---------------------------: | :------------------------------------------------ |
| kubernetes_pod_network | "10.244.0.0/16"               | Pod network CIDR used in kubeadm init             |
| docker_runtime         | False                         | Choose if Docker should be used as runtime        |   
| containerd_runtime     | False                         | Choose if Containerd should be used as runtime    | 
| crio_runtime           | True                          | Choose if Cri-o should be used as runtime         |
| ubuntu_docker_version  | "5:19.03.11~3-0~ubuntu-focal" | Docker Version if running on Ubuntu/Debian        |
| centos_docker_version  | "19.03.0-3.el7"               | Docker Version if running on CentOS/RHEL          | 
| containerd_version     | "1.2.13-2"                    | Containerd version                                | 
| crio_version           | "1.20"                        | Cri-o version                                     |
| kubelet_version        | "1.20.5-00"                   | Kubelet version                                   |
| kubeadm_version        | "1.20.5-00"                   | Kubeadm version                                   |       
| kubectl_version        | "1.20.5-00"                   | Kubectl version                                   |   

&nbsp;
## Contributing
Feel free to create pull requests.

todo systemctl as handler