# Kubernetes Projects on k3s (Gcore Cloud)

Production-grade Kubernetes deployments on a self-managed k3s cluster running on Gcore Cloud VM (Amsterdam).

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
- Custom Docker image — baked HTML, CSS, assets
- Nginx custom config — caching headers, redirect handling

Apply:
kubectl apply -f nginx/deployment.yaml
kubectl apply -f nginx/service.yaml
kubectl apply -f nginx/clusterissuer.yaml
kubectl apply -f nginx/ingress.yaml

Verify:
kubectl get pods
kubectl get svc
kubectl get ingress
kubectl get certificate
curl -I https://testelchin.com

## Nginx Configuration

Custom nginx config baked into Docker image:
- Cache-Control: public, max-age=3600 on home page
- Cache-Control: public, max-age=86400 on universe page
- absolute_redirect off — fixes redirect behind Traefik
- www.testelchin.com + testelchin.com both handled

Verify caching:
curl -I https://testelchin.com
curl -I https://cdn.testelchin.com

Docker image versions:
v1 - initial nginx deployment
v2 - custom HTML pages (home + universe with galaxy background)
v3 - nginx caching config added
v4 - fixed redirect + www support

