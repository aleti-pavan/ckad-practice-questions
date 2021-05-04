
*_Set Configuration Context_*

`kubectl config use-context k8s`

##### (Question)
You are tasked to create a ConfigMap and consume the ConfigMap in a pod using a volume mount.
Task
Please complete the following:

- Create a ConfigMap named _`my-config`_ containing the key/value pair: _`key3/value4`_

- start a pod named _`nginx-configmap`_ containing a single container using the
nginx image, and mount the key you just created into the pod under directory /this/is/mypath


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml

# Create configmap
kubectl create cm my-config --from-literal=key3=value4

# Verify configmap key/value
kubectl describe cm my-config

Output:
------
    Name:         my-config
    Namespace:    default
    Labels:       <none>
    Annotations:  <none>

    Data
    ====
    key3:
    ----
    value4
    Events:  <none>

# Create pod with requested configuration
---
kind: Pod
metadata:
  labels:
    run: nginx-configmap
  name: nginx-configmap
spec:
  volumes:
  - name: myvol
    configMap:
     name: my-config
  containers:
  - image: nginx
    name: nginx-configmap
    volumeMounts:
      - name: myvol
        mountPath: /this/is/mypath
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

# Validate the path created
kubectl exec nginx-configmap -- cat /this/is/mypath/key3

Output:
------
    value4
```

</details>