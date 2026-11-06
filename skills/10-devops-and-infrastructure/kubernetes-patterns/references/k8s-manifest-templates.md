# Kubernetes Manifest Templates & Hardening Specifications (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `kubernetes-patterns`  
> Domain: 10 — DevOps & Infrastructure  

---

## 1. Overview
Hardened, production-grade Kubernetes manifest templates including Deployments, Services, HorizontalPodAutoscalers (HPA), NetworkPolicies, and PodDisruptionBudgets (PDB). Load this reference only when generating or auditing K8s YAML manifests.

---

## 2. Hardened Production Deployment Manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-service
  labels:
    app.kubernetes.io/name: api-service
    app.kubernetes.io/part-of: core-platform
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 0
  selector:
    matchLabels:
      app.kubernetes.io/name: api-service
  template:
    metadata:
      labels:
        app.kubernetes.io/name: api-service
    spec:
      securityContext:
        runAsNonRoot: true
        runAsUser: 10001
        runAsGroup: 10001
        fsGroup: 10001
        seccompProfile:
          type: RuntimeDefault
      containers:
        - name: app
          image: ghcr.io/org/api-service:v1.2.0
          securityContext:
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            capabilities:
              drop: ["ALL"]
          resources:
            requests:
              cpu: 250m
              memory: 256Mi
            limits:
              cpu: 1000m
              memory: 512Mi
          livenessProbe:
            httpGet:
              path: /healthz
              port: 8080
            initialDelaySeconds: 15
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /ready
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
```

