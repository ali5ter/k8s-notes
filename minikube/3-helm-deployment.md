# Using helm to deploy an application on your cluster
Just as a package manager helps you install and upgrade applications on your
operating system, [Helm](https://helm.sh/) helps you install and upgrade
complex applications on Kubernetes. Helm is a package manager for Kubernetes.

It's useful to understand how to use Helm to stand up a popular application
you K8s cluster. We will use Helm to install [Jenkins](https://jenkins.io/), a
popular automation server used by software development teams.

1. Install helm using homebrew using
```shell
brew install kubernetes-helm
```
2. To make it easier enter helm commands, you can install tab or autocompletion
   using
```shell
source <(helm completion bash)
```
3. So Helm can work, the helm agent, tiller, needs to be installed on your
   local cluster. This is called initializing helm.
```shell
$ helm init
Creating /Users/bowena/.helm
Creating /Users/bowena/.helm/repository
Creating /Users/bowena/.helm/repository/cache
Creating /Users/bowena/.helm/repository/local
Creating /Users/bowena/.helm/plugins
Creating /Users/bowena/.helm/starters
Creating /Users/bowena/.helm/cache/archive
Creating /Users/bowena/.helm/repository/repositories.yaml
$HELM_HOME has been configured at /Users/bowena/.helm.

Tiller (the helm server side component) has been installed into your Kubernetes Cluster.
Happy Helming!
```
4. Like any other package manager, you can search for the package (or Helm
   Chart) you want to install. Search for the Helm Chart that installs Jenkins
   using
```shell
$ helm search jenkins
NAME          	VERSION	DESCRIPTION
stable/jenkins	0.8.1  	Open source continuous integration server. It s...
```
5. Deploy the Jenkins chart and check it's status
```shell
〉helm install stable/jenkins
NAME:   pondering-lamb
LAST DEPLOYED: Wed Jul 12 13:21:43 2017
NAMESPACE: default
STATUS: DEPLOYED
```
TODO: More about inspecting the deployment, accessing the application and cleaning up