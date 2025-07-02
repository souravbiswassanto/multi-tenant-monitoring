# infra-setup



# Setup Prometheus and Grafana

```shell
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus -n monitoring prometheus-community/kube-prometheus-stack --create-namespace

```

## Setup multi tenant prometheus

In this setup, we will have a single prometheus scraping all of our tenants metrics.
We will have grafana dashboards for each of the tenants and will make sure none of the
tenant can query other tenants metrics.

### Phase 1: Setup a query-frontier

All of the tenants prometheus query(query that will be written in the form of dashboards) will be proxied by a frontier. 
The query frontier will perform two job,
1. It checks if the pod has the permission to query data from the namespace which he is trying to access
2. Insert a namespace label to the query

#### Description of part 1





from charts/monitoring/values.yaml

```yaml
tenants:
  - name: tenant1
    namespace: acme-dev
  - name: tenant2
    namespace: acme-prod
```

You can add all the tenants in the values file. This helm chart will create
grafana deployment for each