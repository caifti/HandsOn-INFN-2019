# Kubernetes and HTC on demand hands on
![travis build](https://travis-ci.org/DODAS-TS/HandsOn-INFN-2019.svg?branch=master)

## Contacts

Diego Ciangottini (diego.ciangottini<at\>pg.infn.it)


## Acknowledgements / prior work

- [Kubernetes official tutorial](https://kubernetes.io/docs/tutorials)
- [Kubernetes by examples](http://kubernetesbyexample.com/)

## Before starting

1. Log into the dedicated machine (if want to reproduce it at home you can find the Ansible playbooks in this repo)
2. Clone the current repo in your home directory:
```bash
git clone https://github.com/DODAS-TS/HandsOn-INFN-2019.git && cd HandsOn-INFN-2019
```
3. set the environment variable to use the k8s config file pointing to the demo cluster
```bash
export KUBECONFIG=/home/centos/user01/kubeconfig.yml
```

You should now be able to see the cluster nodes with:

```bash
$ kubectl get node
```
```text
NAME                  STATUS   ROLES    AGE     VERSION
vnode-0.localdomain   Ready    master   2d15h   v1.14.0
vnode-1.localdomain   Ready    <none>   2d15h   v1.14.0
vnode-2.localdomain   Ready    <none>   2d15h   v1.14.0
vnode-3.localdomain   Ready    <none>   2d15h   v1.14.0
vnode-4.localdomain   Ready    <none>   2d15h   v1.14.0
```

And to inspect one of them with:

```bash
kubectl describe node vnode-1.localdomain
```

If so, you are ready to start.

## Hands-on guide

- Kubernetes mini tutorial
    - [Overview](k8s/overview.md)
    - [Pods](k8s/pods.md)
    - [Services](k8s/services.md)
- HTCondor on demand:
    - [Deployment](htcondor/configuration.md)
    - [Templating](htcondor/orchent.md)

## EXTRAS

- [Ansible deployment of a webserver](extras/ansible.md)
- [PaaS Orchestrator](extras/orchent.md)

