# Hnds-On Opentelemetry


### 1. Create a cluster named project, using the provided kind cluster config file

kind create cluster --name=project --config=kind-cluster.yaml

### 2. Confirm the cluster node is running

```bash
kubectl get nodes
```

## Deploying Initial Resources

### 3. Deploy cert-manager

Opentelemetry uses the cert-manager to provision TLS certificcates for admission webhooks

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.15.2/cert-manager.yaml

check your and confirm your cert-manager pods are running

kubectl get pods -n cert-manager -w

### 4. Deploy OpenTelemetry Operator

```bash
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.94.0/opentelemetry-operator.yaml
```

Confirm your services are running

```bash
kubectl get pods -n opentelemetry-operator-system -w
```

### 5. Deploy the starter app

#### About The Application
This demo microservice application  is a ....

This is where you get your app backend and pods running.

### 6. Deploy Backend for Observability

This backend deployment config for observability contains the following resources: 
Namespace Config  (observability-backend)
Prometheus ConfigMap
Prometheus Deployment
Prometheus Service
Jaeger ServiceAccount
Jaeger Sampling ConfigMap
Jager Collector
Jaeger Operator
Jaeger Deployment

All deployed in the Observability-backend namespace

```bash
kubectl apply -f app/backend_01.yaml
```

Forward the port so we you can access the app

```bash
kubectl port-forward -n observability-backend service/jaeger-query 16686:16686
```
Open it in the browser localhost:16686

### Deploy the main app into Kubernetes


kubectl apply -f app/k8s.yaml


kubectl get pods -n tutorial-application -w









