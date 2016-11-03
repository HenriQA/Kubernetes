# Kubernetes Installation

##Pre-requisites
 - OS System. Kubernetes works best when it's installed on:
   - Ubuntu 16.04
   - CentOS
   - HypriotOS v1.0.1
 - 1GB of RAM per machiene
 - Full network connectivity between all machines in the cluster
 
##Steps for installing on Ubuntu 16.04 
######(for other OS follow guide on http://kubernetes.io/docs/getting-started-guides/kubeadm/)
### 1. Install Packages
  Become root (`sudo su -`), and tun the following script (on all your nodes):
```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
apt-get update
# Install docker if you don't have it already.
apt-get install -y docker.io
apt-get install -y kubelet kubeadm kubectl kubernetes-cni
```
  This will install:
   a. docker
   b. kubelet
   c. kubeadm
   d. kubectl
### 2. Initialise the master
  Choose a machine to be your master and run:
   ```
   kubeadm init
   ```
  Make a note of the final line (`kubeadm join --token <token> <master-ip>`). You will use this kubeadm join command to add nodes to your master.
### 3. Installing a pod network
  You now need to install a pod network. This will let your pods communicate with each other accross nodes as well as start kube-dns.
  
  To install the "Weave Net" add-on run:
  ```
  kubectl create -f https://git.io/weave-kube
  ```
  More Kubernetes add-ons can be found on this page http://kubernetes.io/docs/admin/addons/
  
  kube-dns should now be up and running! To check it is run `kubectl get pods --all-namespaces` (it may take a few seconds to start)
### 4. Connect nodes to the master
  To connect a node to the master run:
  ```
  kubeadm join --token <token> <master-ip>
  ```
  (this is the one you saved earlier)
  
  On the master you can check to see which nodes are connected by running `kubectl get nodes` on the master.
