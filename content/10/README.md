
*_Set Configuration Context_*

`kubectl config use-context nk8s`

##### (Question)

Task

Please complete the following:

- Create a namespace with name _`debug`_

- Create a deployment called _`debug-deployment`_ with file located at content/10/debug-deployment.yaml

- See why the deployment isn't working and fix it. 

- Make sure all the pods are into running state. 


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml

#Alias k=kubectl
alias k=kubectl

# Create namespace 
k create ns debug

# Change context to debug namespace
k config set-context --current --namespace=debug

# Find and fix the issue
k get deploy 

k get po

# Verify the image
k describe deploy debug-deployment | grep -i "image:"

   Output:- Image:        busyboxx

# Update the image and add command to busybox to have it running.

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: debug-deployment
  name: debug-deployment
  namespace: debug
spec:
  replicas: 3
  selector:
    matchLabels:
      app: debug-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: debug-deployment
    spec:
      containers:
      - image: busybox
        command: ["/bin/sh"]
        args: ["-c", "while true; do sleep 10;done"]
        name: busyboxx
status: {}

k delete debug-deployment; k apply -f debug-deployment.yaml


```

</details>