# Test a deployment on your local Kubernetes cluster
1. Download a yaml file to deploy the minikube sample app using
```shell
curl https://raw.githubusercontent.com/ali5ter/k8s-notes/master/minikube/hello-minikube.yaml -o /tmp/hello-minikube.yaml
```
2. Deploy this sample app using
```shell
kubectl apply -f /tmp/hello-minikube.yaml
```
3. Check to see if the pod that contains to deployed sample app is running
```shell
$ kubectl get services hello-minikube
NAME             TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
hello-minikube   NodePort   10.102.181.116   <none>        80:30036/TCP   10s
```
4. Connect to the sample app 
```shell
$ curl $(minikube service hello-minikube --url)
CLIENT VALUES:
client_address=172.17.0.1
command=GET
real path=/
query=nil
request_version=1.1
request_uri=http://172.16.65.154:8080/

SERVER VALUES:
server_version=nginx: 1.10.0 - lua: 10001

HEADERS RECEIVED:
accept=*/*
host=172.16.65.154:30036
user-agent=curl/7.54.0
BODY:
-no body in request-
```
5. Explore how your deployment looks with the kubernetes dashboard UI using
```shell
minikube dashboard
```
6. To remove the deployment run the following
```shell
kubectl delete service hello-minikube && kubectl delete deployments hello-minikube
```