# EKSCTL CONFIGS

This repository holds all config files needed for creating a simple EKS cluster running
some devops utils like a gitlab runner.

# Tools
- eksctl
- kubectl
- helm
- helmfile

# Helm Plugin
to use the `helmfile` command you need the helm diff plugin
install it with
```bash
$ helm plugin install https://github.com/databus23/helm-diff
```

# Get started
```bash
$ eksctl create -f ./devops-utils-cluster.yaml
```


## apply helm
befor you can deploy the prometheus (with Grafana) helmchart you need to create some CRD in you cluster.
Use the command down below to apply the `kustomization` files
```bash
$ kubectl apply --server-side -k manifests/prometheus
```

To deploy the helmcharts to your cluster use `helmfile`
```bash
$ helmfile apply
```

# Working with eksctl

to change something on the fargate configuration, delete and then recreate the fargate profile based on your new configuratino
```bash
$ eksctl delete fargateprofile --cluster devops-utils <name-of-fargate-profile>
```

Recreate the fargate cluster
```bash
$ eksctl create fargateprofile -f devops-utils-cluster.yaml
```