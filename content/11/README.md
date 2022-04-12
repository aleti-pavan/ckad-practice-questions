
*_Set Configuration Context_*

`kubectl config use-context dk8s`

##### (Question)

Task

Please complete the following:

- create web1 pods using _`web1.yaml`_ in the current directory

- restrict traffic to pod _`db`_ allows traffic from only pods with labels _`tier: db and tier: web`_

<details>
<summary>
Solution - Click to expand!
</summary>

```yaml

#Alias k=kubectl
alias k=kubectl

# Apply the file
k apply -f web1.yaml

# db-ingress-web.yaml

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-ingress-web
spec:
  podSelector:
    matchLabels:
      tier: db
  policyTypes:
  - Ingress
  ingress:
    - from:
      - podSelector:
          matchLabels:
            tier: web
      ports:
        - port: 3306
          protocol: TCP

k apply -f db-ingress-web.yaml
  
```

</details>
