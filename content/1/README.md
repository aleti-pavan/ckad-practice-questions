
*_Set Configuration Context_*

`kubectl config use-context nk8s`

You are tasked to create a secret and consume the secret in pod using environment variables as follow:

TasK

- Create a secret named `my-secret` with a key/value pair; `key2/value10`

- Start an nginx pod named `nginx-secret` using container image `nginx`, and add an environment variable
exposing the value of the secret key key 2, using TEST_VARIABLE as the name for the environment
variable inside the pod


##### [(Solution)](solution.md)

<details>
<summary>
Solution - Click to expand!
</summary>

```yaml
# Create secret
kubectl create secret generic my-secret --from-literal=key2=value10

# Create nginx pod
kubectl run nginx-secret --image=nginx --restart=Never --dry-run=client -o yaml > nginx-secret.yaml

# Update the nginx-secret.yaml like below
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-secret
  name: nginx-secret
spec:
  containers:
  - image: nginx
    name: nginx-secret
    resources: {}
    env: 
    - name: TEST_VARIABLE  #Env Variable Name
      valueFrom:
          secretKeyRef:
            name: my-secret  #Secret Name
            key: key2        #Key in the secret
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

# Apply the updated file
kubectl apply -f nginx-secret.yaml

# Verify the with below command - This should display TEST_VARIABLE with correct value belong to the key

kubectl exec nginx-secret -- env

# OUTPUT - similar to below
HOSTNAME=nginx-secret
TEST_VARIABLE=value10


```

</details>