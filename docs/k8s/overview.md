# Why Kubernetes?

## The evolution of server setups
[![Server standard architecture](img/what_is_kubernetes.png)](https://dodas-ts.github.io/SOSC-2018/k8s/img/what_is_kubernetes.png)

## What will Kubernetes do for you?

- APIs:
    - Kubernetes is driven by its API. Your CI/CD system can communicate with Kubernetes via its REST and CLI interfaces to carry out actions within the cluster. You can build staging environments. You can automatically deploy new releases.
- Failure recovering:
    - Kubernetes monitors the containers running within it, performing readiness and health checks via TCP, HTTP, or by running a command within the container. Only healthy resources receive traffic, and those that fail health checks for too long will be restarted by Kubernetes or moved to other nodes in the cluster.
- Scale automatically.
- Born with microservices in mind.
- Declarative model:
    - The Kubernetes model is declarative. You create instructions in YAML that tell it the desired state of the cluster. It then does what it needs to do to maintain this state. 
- Kubernetes is everywhere:
    - You can run it on bare metal servers or in a private cloud. You can run it on the public cloud. You can run applications within a hosted Kubernetes service.
