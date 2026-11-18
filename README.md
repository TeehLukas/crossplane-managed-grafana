# Crossplane Managed Grafana

Das Taskfile enthält den Bootstrap für den lokalen Kind-Cluster mit Crossplane und Argo CD sowie einen separaten Task für eine lokale Grafana-Instanz.

```text
.
├── Taskfile.yml
├── api/
│   ├── xrds/                # CompositeResourceDefinitions für die Grafana-API
│   └── compositions/        # Pipelines, die function-kcl aufrufen
├── argocd/
│   ├── bootstrap/           # Einstiegspunkt für Argo CD
│   └── applications/        # Argo-CD-Applications und Sync-Reihenfolge
├── crossplane/
│   ├── providers/           # Crossplane-Provider
│   │   └── configs/         # ProviderConfigs mit Referenzen auf Kubernetes-Secrets
│   ├── functions/           # Installation von function-kcl
│   └── grafana/
│       └── kcl/             # KCL-Quellcode für die Compositions
└── environments/
    └── lab/
        └── grafana/         # Konkrete Grafana-Ressourcen für das lokale Lab
```

Argo CD synchronisiert zuerst Provider und Funktionen, dann ProviderConfigs und XRDs, anschließend Compositions und zuletzt die Composite Resources aus `environments/lab/grafana/`. Die Compositions führen KCL über `function-kcl` aus. Der Ordner `crossplane/grafana/kcl/` dient als Ablage für den KCL-Quellcode, den die Compositions später einbinden.
