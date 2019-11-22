# Introduction to pods

## From container to pods

![Kubernete pods schema](img/k8s_deployment.png)

Let's see how we can deploy a simple container using kubernetes. 
To do this we need to introduce 2 k8s resources:

- __Pod__:
    - A pod is a collection of containers sharing a network and mount namespace and is the basic unit of deployment in Kubernetes. All containers in a pod are scheduled on the same node. 
- __Deployment__:
    - A deployment is a supervisor for pods, giving you fine-grained control over how and when a new pod version is rolled out as well as rolled back to a previous state.

### Pod creation

#### Create a pod with kubectl

To run a pod all you need is:

```bash
kubectl run <your pod name> --image=<your container image name> --port=<port to expose>
```

If everything went well you can then see your pod running after a while:

```bash
 kubectl get pods
```
```text
NAME                      READY     STATUS    RESTARTS   AGE
<your pod name>-3210265840-k705b     1/1       Running   0          1m
```

You can see that a deployment has been created automaticcaly to supervise the pod:

```bash
 kubectl get deployments
```

#### Inspect resources
Every k8s resource can be inspected with the command `describe`. This will provide you with a variety of useful information on the state and cofiguration of the resource. For instance you can get the internal cluster IP of the running container in the pod.

```bash
kubectl describe pod <your pod name>-3210265840-k705b | grep IP:
IP:                     172.17.0.3
```

#### Using configuration files

Any resource can also be created from a yaml or json template. 
In case of a pod you can find the configuration file in `templates/pods.yml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configuredpod
spec:
  containers:
  - name: <my configured name>
    image: <your container image name>
    ports:
    - containerPort: 9876
    resources:
      limits:
        memory: "64Mi"
        cpu: "500m"
```

As you can see, is also possible to set limits for the resource to be reserved for the pod. 

Now the syntax for creating a resource from a file is:

```bash
kubectl create -f templates/pods.yml
```


#### Create a deployment from configuration file

You can find the configuration file for a deployment in `templates/deployments.yml`:

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: my-deploy
spec:
  replicas: 2
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: <conta>
        image: <container image name>
        ports:
        - containerPort: 9876
        env:
        - name: SIMPLE_SERVICE_VERSION
          value: "1.0"
```

Here you can see the addition of the `replica` field where you can specifiy how many replicas of the same file you want.
Also the `label` metadata is important to organize the application management as we will see next on the k8s `service` section.


### Delete 

Delete the two pods and pay attention to what happens.

``` bash
kubectl delete pod <pod name>
```

__Hint__: remember that also a deployment has been created

[TODO: ESEMPIO RESTART E PERDITA DATI]