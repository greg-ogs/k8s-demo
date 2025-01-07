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

Task 10(advanced)

Create a static pod.

Requirements:

Pod name: nginx-static
Pod image: nginx:alpine
Pod label: app=nginx-static
Namespace: static
Container Port: 80
How to verify: Try to delete static pod. It should be recreated

Do not forget to copy secret phrase, test will fail after next task.

Task 11(advanced):

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

