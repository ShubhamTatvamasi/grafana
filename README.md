# grafana

https://grafana.com/grafana/dashboards/

add helm repo:
```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

install grafana:
```bash
helm upgrade -i grafana grafana/grafana \
  --create-namespace \
  --namespace grafana \
  --set service.type=NodePort \
  --set persistence.enabled=true \
  --set service.nodePort=30000
```

update password for `admin` user:
```bash
kubectl patch secret grafana -n grafana \
  --patch='{"data": {"admin-password": "YWRtaW4="}}'

# get password for admin user:
kubectl get secret --namespace grafana grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

datasource:
```
http://prometheus.lens-metrics.svc.cluster.local
```

Dashboard | ID
--- | --- 
Node Exporter Full | 1860
Kubernetes / Views / Pods | 15760
Istio Control Plane Dashboard | 7645
Istio Service Dashboard | 7636
Istio Workload Dashboard | 7630
Istio Mesh Dashboard | 7639


