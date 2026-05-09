# Kubernetes Projects on k3s (Gcore Cloud)

Production-grade Kubernetes deployments on a self-managed k3s cluster running on Gcore Cloud VM.

## Infrastructure

Cloud: Gcore Cloud VM — 4 vCPU, 8GB RAM, 50GB SSD
Kubernetes: k3s v1.35
Ingress Controller: Traefik
SSL: cert-manager + Let's Encrypt

---

## Project 1 — Nginx with SSL

Live deployment of Nginx on Kubernetes with real domain and HTTPS.

Live: https://testelchin.com

Components:
- Deployment — 2 replicas, resource requests and limits
- ClusterIP Service — internal load balancing
- Traefik Ingress — domain routing
- cert-manager ClusterIssuer — automatic SSL from Let's Encrypt

Apply:
kubectl apply -f nginx/deployment.yaml
kubectl apply -f nginx/service.yaml
kubectl apply -f nginx/clusterissuer.yaml
kubectl apply -f nginx/ingress.yaml

Verify:
kubectl apply -f nginx/deployment.yaml
kubectl get pods
kubectl get svc
kubectl get ingress
kubectl get certificate
curl -I https://testelchin.com
