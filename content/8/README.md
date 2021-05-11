
*_Set Configuration Context_*

`kubectl config use-context rk8s`

##### (Question)
You are tasked to create a pv, pvc and attach it to a pod.

Task

Please complete the following:

- create a pv named `_task-pv-volume_` with storage `_10Gi_` , access modes `_ReadWriteOnce_` , torageClassName `_manual_` and volume at /my/path and verify

- Create a PersistentVolumeClaim of at least `_3Gi_` storage and access mode `_ReadWriteOnce_` and verify status is `_Bound_`

- Create an nginx pod with containerPort `_80_` and with a PersistentVolumeClaim task-pv-claim and has a mouth path `_"/usr/share/nginx/html"_`


details>
<summary>
Solution - Click to expand!
</summary>

```yaml

#Alias k=kubectl
alias k=kubectl

# task-pv-volume.yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: task-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/my/path"

# Apply and verify
k apply -f task-pv-volume.yaml ; k get pv

# task-pv-claim.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi

k apply -f task-pv-claim.yaml ; k get pvc

# task-pv-pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: task-pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage

k apply -f task-pv-pod.yaml

```

</details>