
# Debugging in Kubernetes

## Visualize container logs 

Logging is one option to understand what is going on inside your applications and the cluster at large. Basic logging in Kubernetes makes the output a container produces available, which is a good use case for debugging. More advanced setups consider logs across nodes and store them in a central place, either within the cluster or via a dedicated (cloud-based) service.

### Kubectl logs

kubectl logs --tail=5 logme -c gen

kubectl logs -f --since=10s logme -c gen

### Edit resources

kubectl edit deployment ...

## Extras
### WebUI

#### Login and tabs

https://193.204.89.106:30443/#!/deployment?namespace=form<your ID>

Get your token:

```bash
$ kubectl describe serviceaccount form<your ID> | grep Tokens
Tokens:              form<your ID>-token-2fbz
```
```bash
$ kubectl describe secret form<your ID>-token-2fbz8 | grep token: 
token:      eyJhbG.......
```