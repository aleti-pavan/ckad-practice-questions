
*_Set Configuration Context_*

`kubectl config use-context nk8s`

You are tasked to create a secret and consume the secret in pod using environment variables as follow:
TasK
- Create a secret named `my-secret` with a key/value pair; `key2/value10`
- Start an nginx pod named `my-secret` using container image `nginx`, and add an environment variable
exposing the value of the secret key key 2, using TEST_VARIABLE as the name for the environment
variable inside the pod

