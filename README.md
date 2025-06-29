# infra-setup

We should write infra setup related information here


# Setup Prometheus and Grafana

```shell
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus -n monitoring prometheus-community/kube-prometheus-stack --create-namespace

```
