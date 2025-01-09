# Kubernetes demo
This repo has the kubernetes concept demo for **PODS, Deployments, StatefulSets, DaemonSets, services and Ingress**

## PODS
The **pods.yml** file contains the tasks for pods creations.
### Task 1:
You should create a pod by following the requirements:
- **Pod Name**: `nginx-pod`
- **Pod Image**: `nginx:alpine`
- **Pod Label**: `app=nginx`
- **Namespace**: `default`
- **Container Port**: `80`

### Task 2:
Please find a pod called **save-me** and save its manifest (yaml output format) to `$HOME/k8s_pods/save-me-pod.yml`.

## Task 3:
A new Pod **web** has been deployed in **namespace**: `trouble`. It has failed. Please find it, figure out the reason and fix it.

**Requirements**:

- **Image**: `nginx:1.19-alpine`
- **Pod Status**: `Running`

### Task 4:
A new **redis-db** pod has been deployed in namespace trouble. It failed. Please fix it.

### Task 5:
Create a new pod named **redis** with `redis:123` image. And yes, the image name is wrong!

**Requirements**:

- **Name**: `redis`
- **Image Name**: `redis:123`
- **Namespace**: `default`
Do not forget to copy secret phrase, test will fail after next task.

### Task 6:
Now please change that redis pod image to the correct version.

**Requirements**:

- **Name**: `redis`
- **Image Name**: `redis:5-alpine`

### Task 7:
Create a Pod (namespace: default, name: envtest, image: busybox:1.34, container process: env && sleep infinity). 
Specify the following ENV variables for the main container:

`STUDENT_FIRST_NAME: <yourname>`
`STUDENT_LAST_NAME: <yourlastname>`
Check Pod logs with `kubectl` logs command. Should be similar to this:
```
... 
STUDENT_FIRST_NAME=Ivan 
STUDENT_LAST_NAME=Ivanov 
...
```
Save actual POD’s logs (full output) into `$HOME/k8s_pods/default-envtest.log` file

### Task 8 (advanced):
Create a Pod (namespace: default, name: i-know-who-i-am, image: busybox:1.34, container process: env && sleep infinity). Specify following ENV variables for the main container:

`MY_NODE_NAME` should contain name of pod node
`MY_POD_NAME` should contain name of pod (do not provide it manually)
`MY_POD_NAMESPACE` should contain name of pod namespace (do not provide it manually)
`MY_POD_IP` should contain pod IP address
`MY_POD_SERVICE_ACCOUNT` should contain a pod service account


### Task 9:
Delete all pods in clean-up namespace.

### Task 10(advanced)

Create a static pod.

Requirements:

Pod name: nginx-static
Pod image: nginx:alpine
Pod label: app=nginx-static
Namespace: static
Container Port: 80
How to verify: Try to delete static pod. It should be recreated

Do not forget to copy secret phrase, test will fail after next task.

### Task 11(advanced):

Delete a static pod nginx-static

## Deployments

### Task 1:
Create a new deployment called nginx-deploy:

Requirements:
 Name: nginx-deploy
 Image: nginx:1.19-alpine
 Namespace: default
 Replicas: 1
 Labels: app=nginx-deploy
Do not forget to copy secret phrase, test will fail after task 3.

### Task 2:
Inspect the details listed below, add necessary options to kubectl create deploy command to produce following deployment configuration:

Name: easy-peasy
Image: busybox:1.34
Replicas: 5
Command: sleep infinity
### Task 3:
Scale nginx-deploy deployment to 6 replicas.

### Task 4:
Inspect the details listed below and create deployment:

Deployment Name: <youname>-app
Replicas: 1
Deployment Labels:
  task: deploy
  app: <youname>-app
  student: <youname>
Pod(s) Labels:
   deploy: <youname>-app
   kind: redis
   role: master
   tier: db
Container:
   Image: redis:5-alpine
   Port: 6379
   Name: redis-master
Init Container:
   Image: busybox:1.34
   Command: sleep 10

### Task 5:
Current deployment nginx-deploy release has nginx:1.19-alpine image.New release should use nginx:1.21-alpine.Use rolling update process

### Task 6:
A lemon deployment has been deployed in namespace trouble, but there are no pods associated with it. Figure out the root cause and fix the issue.

### Task 7:
A orange deployment has been deployed in namespace trouble, but it doesn’t work properly. Figure out the root cause and fix the issue.

## StatefulSets 

### Task 1:

Create a new **StatefulSet**:

**Requirements**:
 - **Name**: `random-generator`
 - **Image**: `sbeliakou/random-generator:1`
 - **Namespace**: `default`
 - **Replicas**: `3`
 - **Service**: `random-generator`
 - **Labels**: `app=random-generator`
Do not forget to copy secret phrase, test will fail after task 3.

### Task 2:

Add volumeClaimTemplates to random-generator sts. Recreate statefulset if it’s needed.

- **Name**: `logs`
- **mountPath**: `/logs`
Capacity: 10Mi
accessMode: ReadWriteOnce

### Task 3:
Update container’s image to version `2`.
Please pay attention to the way how StatefulSet recreates pods. It starts from 2 and goes to 0.

### Task 4:

Run any test pod. Using nslookup check the record of random-generator service. Save the output of the 
below commands to `$HOME/k8s_sts.tx`t
```
nslookup random-generator-0.random-generator.default.svc.cluster.local
nslookup random-generator-1.random-generator.default.svc.cluster.local
nslookup random-generator-2.random-generator.default.svc.cluster.local
```


## DaemonSets

### Task 1:

Create a new node and set up a **worker** role for it.

Remember to copy secret phrase, test will fail after task 5.

### Task 2:
Taint your nodes.

**Requirements**:
- **control-plane**:
    - _key_: `node-role.kubernetes.io/control-plane`
    - _effect_: `NoSchedule`
- **worker**:
  - key: `node-role.kubernetes.io/worker`
  - effect: `NoSchedule`
Do not forget to copy secret phrase, test will fail after task 6.

### Task 3:

Deploy **daemonset**

**Requirements**:
- **Name**: `fluentd-elasticsearch`
- **Image**: `quay.io/fluentd_elasticsearch/fluentd:v4`
Please pay attention how many pods were created and why.

Do not forget to copy secret phrase, test will fail after next task.

### Task 4:

Modify **fluentd-elasticsearch** _*DaemonSet*_ to ensure that pods run on every **node**.You should change only DaemonSet configuration!

Do not forget to copy secret phrase, test will fail after next task.

### Task 5:

Create one more node and set up **worker** role for it.

Please pay attention on number of pods.

Do not forget to copy secret phrase, test will fail after task 6.

### Task 6:

jq utility should be installed before running checker!

Get details of nodes in JSON format and save it to `$HOME/nodes-info.json` file.
Delete all worker nodes.
**Untaint** control-plane node.
Remove **fluentd-elasticsearch** _*DaemonSet*_.

## Services

### Task 1:

Create **pod-info-svc** _*service*_ for **pod-info-app** _*deployment*_:

Requirements:
- **Name**: `pod-info-svc`
- **Type**: `ClusterIP`
- **Service Port**: `80`
- **Service TargetPort**: `80`
Investigate **pod-info-app** ***deployment*** and choose selector and do not change the deployment.

### Task 2:

Run a pod (based on image `busybox:1.28`) and execute the following commands (as given below) inside
this pod and save outputs into files:

```
wget -q -O- pod-info-svc  
$HOME/testing-clusterip-web.log
nslookup pod-info-svc
$HOME/testing-clusterip-nslookup.log
```

### Task 3:

Create deployment **myapp**, **image**: `sbeliakou/web-pod-info:v1`, **replicas**: _*1*_
Create **headless service** ***myapp-headless*** pointing to **myapp** pods
Create **non-headless service** ***myapp-clusterip*** pointing to **myapp** pods
Checking name resolution:

Non-headless service has own IP address (and port), and proxies traffic to backends:

```
$ kubectl run --rm -it test --image=busybox:1.27 --restart=Never nslookup myapp-clusterip
```
Headless service doesn’t proxy traffic to backends, it simply responds (on early dns lookup phase) with the IP address(es) where to go:
```
$ kubectl run --rm -it test --image=busybox:1.27 --restart=Never nslookup myapp-headless
```

### Task 4:
We have already created **hello-hello** web application for you. Create a new service to access this web application, 
check the requirements. Figure out all necessary settings from the deployment.

**Requirements**:
- **Name**: `hello-hello-service`
- **Type**: `NodePort`
- **Downstream Pod Port (Service targetPort)**: `80`
- **Node Port**: `30300`
For verification you can execute `curl $NODE_IP:30300` command or open the browser page ***http://$NODE_IP:30300***. 
Substitute `$NODE_IP` with the IP address of your node.