Manifest of modifications to original [click-to-deploy](https://github.com/GoogleCloudPlatform/click-to-deploy/tree/master/k8s/prometheus) repository (`prometheus` corresponds to the click-to-deploy repo): 

```
Only in doks-monitoring/: .git
Only in doks-monitoring/: .gitignore
Only in doks-monitoring/: LICENSE
Only in prometheus/: Makefile
Files prometheus/README.md and doks-monitoring/README.md differ
Only in prometheus/: apptest
Only in prometheus/: deployer
Only in doks-monitoring/manifest: alertmanager-0serviceaccount.yaml
Files prometheus/manifest/alertmanager-statefulset.yaml and doks-monitoring/manifest/alertmanager-statefulset.yaml differ
Only in prometheus/manifest: application.yaml
Files prometheus/manifest/dashboards-configmap.yaml and doks-monitoring/manifest/dashboards-configmap.yaml differ
Only in doks-monitoring/manifest: grafana-0serviceaccount.yaml
Files prometheus/manifest/grafana-statefulset.yaml and doks-monitoring/manifest/grafana-statefulset.yaml differ
Only in doks-monitoring/manifest: kube-state-metrics-0serviceaccount.yaml
Files prometheus/manifest/kube-state-metrics-deployment.yaml and doks-monitoring/manifest/kube-state-metrics-deployment.yaml differ
Only in doks-monitoring/manifest: node-exporter-0serviceaccount.yaml
Files prometheus/manifest/node-exporter-ds.yaml and doks-monitoring/manifest/node-exporter-ds.yaml differ
Only in doks-monitoring/manifest: prometheus-0serviceaccount.yaml
Files prometheus/manifest/prometheus-configmap.yaml and doks-monitoring/manifest/prometheus-configmap.yaml differ
Files prometheus/manifest/prometheus-statefulset.yaml and doks-monitoring/manifest/prometheus-statefulset.yaml differ
Only in prometheus/: resources
Only in prometheus/: schema.yaml
```

High-level overview of changes:
- Use quay.io images instead of GCP Marketplace images:
  - Prometheus: `quay.io/prometheus/prometheus:v2.11.1`
  - Alertmanager: `quay.io/prometheus/alertmanager:v0.16.0`
  - Kube-state-metrics: `quay.io/coreos/kube-state-metrics:v1.5.0`
  - Node-exporter: `quay.io/prometheus/node-exporter:v0.17.0`
  - Grafana: `grafana/grafana:6.0.1`
  - Prometheus-init: `debian:9`
- Modify manifests to work with these images
- Modify prometheus.yaml Prometheus configuration in the Prometheus ConfigMap with a DOKS-specific config
- Regenerate Grafana dashboards, Prometheus Rules, and Alerts using kubernetes-mixin
- Refactor and modify manifests to streamline deployment by hardcoding replica configuration, container images, and Service Accounts
- Remove references to GCP and GCP-specific configuration
