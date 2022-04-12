
*_Set Configuration Context_*

`kubectl config use-context nk8s`

##### (Question)
You are tasked to create a serviceAccount and update the deployment to use created serviceAccount.

Task

Please complete the following:

- Update the app Deployment _`app-deployment`_ in the _`ns-prod`_ Namespace using image _`nginx`_ to run as the _`app-sa`_ ServiceAccount.

- Create the ServiceAccount _`app-sa`_ first.


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml

# Create namespace 
kubectl create ns ns-prod

# Create serviceaccount in the namespace
kubectl create sa app-sa -n ns-prod

# Generate deployment YAML
kubectl create deployment app-deployment -n ns-prod --image=nginx --dry-run=client -o yaml > app-deployment.yaml

# Update the yaml with sa
---
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: app-deployment
  name: app-deployment
  namespace: ns-prod
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app-deployment
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: app-deployment
    spec:
      serviceAccountName: app-sa # service account config
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}

# Verify the sa config 
kubectl describe deploy app-deployment -n ns-prod | grep -i service
  Service Account:  app-sa


```

</details>
