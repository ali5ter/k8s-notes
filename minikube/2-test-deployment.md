# Test a deployment on your local Kubernetes cluster
Now you have your own K8s cluster running on your local system, we will deploy
a super simple sample application on the cluster so we can see the pod and
service that are created to run the application and provide access to it.

1. Download a yaml file to deploy the minikube sample app using
```shell
curl https://raw.githubusercontent.com/ali5ter/k8s-notes/master/minikube/hello-minikube.yaml -o /tmp/hello-minikube.yaml
```
2. Deploy this sample app using
```shell
kubectl apply -f /tmp/hello-minikube.yaml
```
3. Check to see if the pod that contains to deployed sample app is running and
   accesible via the service
```shell
$ kubectl get services hello-minikube
NAME             TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
hello-minikube   NodePort   10.102.181.116   <none>        80:30036/TCP   10s
```
4. Use labels to see the kubernetes objects that make up the sample app
```shell
$ kubectl get all -l app=hello-minikube
NAME                                  READY   STATUS    RESTARTS   AGE
pod/hello-minikube-69c6558555-bngk7   1/1     Running   0          3m18s

NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-minikube   1/1     1            1           3m18s

NAME                                        DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-minikube-69c6558555   1         1         1       3m18s
```
5. Look at the detail of the pod running the sample app container using
```shell
〉kubectl describe pod hello-minikube-69c6558555-fqf8r
Name:               hello-minikube-69c6558555-fqf8r
Namespace:          default
Priority:           0
PriorityClassName:  <none>
Node:               minikube/172.16.65.154
Start Time:         Tue, 09 Jul 2019 13:19:25 -0400
Labels:             app=hello-minikube
                    pod-template-hash=69c6558555
Annotations:        <none>
Status:             Running
IP:                 172.17.0.7
Controlled By:      ReplicaSet/hello-minikube-69c6558555
Containers:
  hello-minikube:
    Container ID:   docker://82e4802a75af5620d4de7ac4ad6944a6b443530ad26da84dff3f93c954ed59f4
    Image:          gcr.io/google_containers/echoserver:1.4
    Image ID:       docker-pullable://gcr.io/google_containers/echoserver@sha256:5d99aa1120524c801bc8c1a7077e8f5ec122ba16b6dda1a5d3826057f67b9bcb
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 09 Jul 2019 13:19:26 -0400
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-zqj9c (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  default-token-zqj9c:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-zqj9c
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  38s   default-scheduler  Successfully assigned default/hello-minikube-69c6558555-fqf8r to minikube
  Normal  Pulled     37s   kubelet, minikube  Container image "gcr.io/google_containers/echoserver:1.4" already present on machine
  Normal  Created    37s   kubelet, minikube  Created container hello-minikube
  Normal  Started    37s   kubelet, minikube  Started container hello-minikube
```
6. Connect to the sample app to test that it responds 
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
7. You can open another terminal window and use the following command to
   'tail' the sample app logs to see your successful connection
```shell
$ kubectl logs $(kubectl get pod -o=name -l app=hello-minikube) -f
172.17.0.1 - - [09/Jul/2019:17:21:51 +0000] "GET / HTTP/1.1" 200 394 "-" "curl/7.54.0"
```
8. Explore how your deployment looks with the kubernetes dashboard UI using
```shell
minikube dashboard
```
9. Use labels to remove the sample app using
```shell
kubectl delete deployment,service -l app=hello-minikube
```