
# Deploying HTCondor on demand 

## Templating an HTCondor k8s cluster: Helm

[Helm](https://helm.sh/) helps managing Kubernetes applications through a standard templating.
The latest version of Helm is maintained by the CNCF - in collaboration with Microsoft, Google, Bitnami and the Helm contributor community. For this hands on we will use the v2 though, since DODAS is currently in the midle of the migration from v2 to v3. 

![Helm motivation](img/helm_love.png)

On [HelmHub](https://hub.helm.sh/) you can find by yourselves the motivation of adopting a widely adopted template format.

Helm uses a packaging format called charts. A chart is a collection of files that describe a related set of Kubernetes resources. A single chart might be used to deploy something simple, like a memcached pod, or something complex, like a full web app stack with HTTP servers, databases, caches, and so on.

### Chart folder tree

Charts are created as files laid out in a particular directory tree, then they can be packaged into versioned archives to be deployed.


```text
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```

### Values

[HELM values](https://github.com/DODAS-TS/HandsOn-INFN-2019/blob/master/htc_helm/values.yaml)

### Templates

- [Ansible role](https://github.com/indigo-dc/ansible-role-htcondor_config)

- [Master/Collector/CCB/negotiator](https://github.com/DODAS-TS/HandsOn-INFN-2019/blob/master/htc_helm/templates/master.yaml)
- [Schedd](https://github.com/DODAS-TS/HandsOn-INFN-2019/blob/master/htc_helm/templates/schedd.yaml)
- [TTS X509 proxy](https://github.com/DODAS-TS/HandsOn-INFN-2019/blob/master/htc_helm/templates/tts.yaml)
- [Worker node](https://github.com/DODAS-TS/HandsOn-INFN-2019/blob/master/htc_helm/templates/wn.yaml)


## Test the deployment



## EXTRA

### try helm standalone

helm template mychart -x templates/deployment.yaml

### integration in ansible

[REF to ansible]