# Deploy a local Kubernetes cluster
Let's stand up a K8s cluster on you local macOS system.

1. Install kubectl using
```shell
brew update && brew install kubectl && kubectl version
```
2. Install minikube on macOS using 
```shell
brew cask install minikube
```
3. To make it easier enter kubectl and minikube commands, you can install tab
   or autocompletion for both commands using
```shell
source <(kubectl completion bash)
source <(minikube completion bash)
```
4. Install the VMware unified driver on macOS using
```shell
export LATEST_VERSION=$(curl -L -s -H 'Accept: application/json' https://github.com/machine-drivers/docker-machine-driver-vmware/releases/latest | sed -e 's/.*"tag_name":"\([^"]*\)".*/\1/') \
&& curl -L -o docker-machine-driver-vmware https://github.com/machine-drivers/docker-machine-driver-vmware/releases/download/$LATEST_VERSION/docker-machine-driver-vmware_darwin_amd64 \
&& chmod +x docker-machine-driver-vmware \
&& mv docker-machine-driver-vmware /usr/local/bin/
```
5. Set up the VMware unified driver as a default driver
```shell
minikube config set vm-driver vmware
```
6. Enable the ingress extension of your local minikube deployed cluster using
```shell
minikube addons enable ingres
```
7. Start up your Kubernetes cluster
```shell
$ minikube start
Starting local Kubernetes v1.6.4 cluster...
Starting VM...
Downloading Minikube ISO
 90.95 MB / 90.95 MB [==============================================] 100.00% 0s
Moving files into cluster...
Setting up certs...
Starting cluster components...
Connecting to cluster...
Setting up kubeconfig...
Kubectl is now configured to use the cluster.
```
8. If you ever want to see if your local K8s cluster is running, check its
   status using
```shell
minikube status
```
9. Explore your cluster with the kubernetes dashboard UI using
```shell
minikube dashboard
```
10. Stop the cluster at any time using
```shell
minikube stop
```
11. To selete the minikube VM use
```shell
minikube delete
```
Note: Deleting the VM means that the next time you do a `minikube start`, a new
VM will need to be created and will take more time that just stopping and restarting.

[Test your cluster by deploying a very simple application...](2-test-deployment.md)