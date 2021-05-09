
*_Set Configuration Context_*

`kubectl config use-context rk8s`

##### (Question)

Task

Please complete the following:

- Create a namespace with name _`development`_

- Create a deployment called _`prod-deployment`_ with image _`nginx`_ and tag _`1.15.9`_ within _`development`_ namesapce, make sure you have _`4 replicas`_ for the deployment

- Set the image to _`nginx:1.13.6`_ and check the status of the deployment

- undo the changes made.


<details>
<summary>
Solution - Click to expand!
</summary>

```yaml

#Alias k=kubectl
alias k=kubectl

# Create namespace 
k create ns development

# Create deployment
k -n development create deploy prod-deployment --image=nginx:1.15.9 --replicas=4

# Verify the image
k describe deploy -n development | grep -i "image:"

   Output:- Image:        nginx:1.15.9

# Update the image
k set image deploy prod-deployment nginx=nginx:1.13.6 -n development

# Verify the image
k describe deploy -n development | grep -i "image:"
  Output:-  Image:        nginx:1.13.6

# Undo the change made
k rollout undo deploy prod-deployment -n development

# Verify the image after rollback
k describe deploy -n development | grep -i "image:"

   Output:- Image:        nginx:1.15.9

```

</details>