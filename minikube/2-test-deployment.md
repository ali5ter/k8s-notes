# Test a deployment on your local Kubernetes cluster
1. Deploy the minikube sample app using
```shell
kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
```
2. Expose the deployed sample app as a service using
```shell
kubectl expose deployment hello-minikube --type=NodePort
```
3. Check to see if the pod that contains to deployed sample app is running
```shell
$ kubectl get services
NAME             CLUSTER-IP   EXTERNAL-IP   PORT(S)          AGE
hello-minikube   10.0.0.224   <nodes>       8080:32581/TCP   16s
kubernetes       10.0.0.1     <none>        443/TCP          3m
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
request_uri=http://172.16.65.128:8080/

SERVER VALUES:
server_version=nginx: 1.10.0 - lua: 10001

HEADERS RECEIVED:
accept=*/*
host=172.16.65.128:30343
user-agent=curl/7.51.0
BODY:
-no body in request-
5. Continue to use kubectl to interact with your cluster and play with the K8s dashboard UI using
```shell
minikube dashboard
```
TODO: Use non-deprecated deployment method