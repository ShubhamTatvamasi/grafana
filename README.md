# grafana

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
  --set service.nodePort=30000
```

get password for `admin` user:
```bash
kubectl get secret --namespace grafana grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

datasource:
```
http://prometheus.lens-metrics.svc.cluster.local
```

Dashboard | ID
--- | --- 
Node Exporter Full | 1860


