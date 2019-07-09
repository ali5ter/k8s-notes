# Why have a local Kubernetes cluster?
Having a kubernetes cluster to play with can really help when learning about
K8s concepts.

Many of [the tutorials found online](https://kubernetes.io/docs/tutorials/)
require that you have access to a K8s cluster, so having K8s running on your
local system, like your laptop, is pretty handy.

[Minikube](https://github.com/kubernetes/minikube) is an application you run on
your laptop. It provides an extremely convenient way to install and configure a
single node K8s in a VM on your local system!

The following guides hope to help you deloy and play with K8s on your local
macOS system.

## Pre-requisites for the guides
* Assumes you're using macOS system
* Assumes [VMware Fusion](https://www.vmware.com/products/fusion.html) is
installed on your macOS system
* Install the [homebrew](https://brew.sh/) package manager

TODO: Remove dependency on Fusion and explain how to use hyperkit driver

## Guides
1. [Start a local cluster](1-deploy-a-local-cluster.md)
2. [Test your cluster with a test deployment](2-test-deployment.md)