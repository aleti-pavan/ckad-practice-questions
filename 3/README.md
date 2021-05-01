
*_Set Configuration Context_*

`kubectl config use-context k8s`

##### (Question)
You are required to create a pod that requests a certain amount of CPU and memory, so it gets scheduled
to-a node that has those resources available.
• Create a pod named nginx-resources in the pod-resources namespace that requests a minimum of
200m CPU and 1Gi memory for its container
• The pod should use the nginx image
• The pod-resources namespace has already been created