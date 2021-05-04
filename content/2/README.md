
*_Set Configuration Context_*

`kubectl config use-context k8s`

Context

A web application requires a specific version of redis to be used as a cache.

Task

Create a pod with the following characteristics, and leave it running when complete:

- The pod must run in the _`frontend`_ namespace. Check if the namespace has already been created and create if necessary

- The name of the pod should be _`cache`_

- Use the _`library/redis`_ image with the _`3.2`_ tag

- Expose port _`6379`_


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml
# Check if namespace exist
kubectl get ns | grep frontend

# Create namespace if not exist
kubectl create ns frontend

# Create pod and expose the given port
kubectl run cache --image=library/redis:3.2 --port 6379 -n frontend

```

</details>