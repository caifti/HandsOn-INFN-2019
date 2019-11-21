# Exposing applications in pod

We can create a reliable way to access the enpoint inside a pod using the `service` k8s resource:

- A service is an abstraction for pods, providing a stable, so called virtual IP (VIP) address. While __pods may come and go and with it their IP addresses, a service allows clients to reliably connect to the containers running in the pod using the VIP__. 
    - The virtual in VIP means it is not an actual IP address connected to a network interface, but its purpose is purely to __forward traffic to one or more pods.__
    - Keeping the mapping between the VIP and the pods up-to-date is the job of __kube-proxy, a process that runs on every node,__ which queries the API server to learn about new services in the cluster.


## Create a service


## Using ExternalIPs



## Using NodePort



## Extras: ingress
