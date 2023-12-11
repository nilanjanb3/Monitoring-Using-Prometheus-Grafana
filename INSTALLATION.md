# Prometheus Installation using Helm

## Prerequisites

Ensure that you have the following prerequisites installed:

- [Helm](https://helm.sh/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

## Step 1: Add Prometheus Helm Repository

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

## Step 2: Create a Namespace

```bash
kubectl create ns monitoring

## Step 3: Install Prometheus & Port Forwarding

```bash
helm install poc-prometheus prometheus-community/prometheus -n monitoring
kubectl port-forward -n monitoring svc/poc-prometheus-server 8080:80

## Step 4: Optional Port Forwarding for KSM

```bash
kubectl port-forward -n monitoring svc/poc-prometheus-kube-state-metrics 8081:8080

## Step 5: Install Grafana & Port Forwarding

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm install poc-grafana grafana/grafana -n monitoring

kubectl port-forward -n monitoring svc/poc-grafana 8082:80

kubectl get secret poc-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 -d

