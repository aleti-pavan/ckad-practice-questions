
*_Set Configuration Context_*

`kubectl config use-context rk8s`

##### (Question)
You are tasked to write logs of _`second`_ container in the pod _`app`_ and write to file _`/app/second.log`_

Task

Please complete the following:

- Create a pod _`app`_ with two containers, first container _`busybox`_ image  and second container _`nginx`_ image .

- Check if the file _`./app/second.log`_ is already created and create if needed.


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml

#Alias k=kubectl
alias k=kubectl

# Check and create path if needed
mkdir ./app

#Generate yaml file
k run app --image=busybox --dry-run=client -o yaml > app.yaml

# Create pod with two containers.
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: app
  name: app
spec:
  containers:
  - image: busybox
    name: first
  - name: second
    image: nginx

# Save the logs to given path
k logs app -c second > ./app/second.log

# Validate the file if it containes logs
cat ./app/second.log 

Output:
--------
        /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
        /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
        /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
        10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
        10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
        /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
        /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
        /docker-entrypoint.sh: Configuration complete; ready for start up

```

</details>