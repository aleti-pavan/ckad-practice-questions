
*_Set Configuration Context_*

`kubectl config use-context k8s`

##### (Question)
You are required to create a pod that requests a certain amount of CPU and memory, so it gets scheduled
to-a node that has those resources available.

- Create a deployment named `pod-resources` in the `resources` namespace that requests a minimum of
300m CPU and 1Gi memory for its container

- The pod should use the `nginx` image

- Check if the `resources` namespace has already been created


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml
# Check if namespace exist
kubectl get ns | grep resources

# Create namespace if not exist
kubectl create ns resources

# Create pod with requested configuration
kubectl run pod-resources -n resources --image=nginx --requests=cpu=300m,memory=1Gi

#Verify the configuration
kubectl describe po pod-resources -n resources | grep -i cpu
      cpu:        300m

kubectl describe po pod-resources -n resources | grep -i memory
      memory:     1Gi

kubectl describe po pod-resources -n resources | grep -i "image:"
    Image:          nginx

```

</details>