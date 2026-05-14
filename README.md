# Kubernetes Projects on k3s (Gcore Cloud)

Kubernetes deployments on a self-managed k3s cluster running on Gcore Cloud VM.

## Infrastructure

Cloud: Gcore Cloud VM — 4 vCPU, 8GB RAM, 50GB SSD
Kubernetes: k3s v1.35
Ingress Controller: Traefik
SSL: cert-manager + Let's Encrypt

---

## Project 1 — Nginx as CDN Origin

Live Nginx deployment on Kubernetes configured as origin for Gcore CDN.

Origin Live : https://testelchin.com
CDN: https://cdn.testelchin.com

Components:
- Deployment — 2 replicas, resource requests and limits
- ClusterIP Service — internal load balancing
- Traefik Ingress — domain routing for testelchin.com and www.testelchin.com
- cert-manager ClusterIssuer — automatic SSL from Let's Encrypt (SAN certificate)
- Custom Docker image — baked HTML, CSS, images
- Nginx custom config — caching, security headers, rate limiting, error pages

## Nginx Configuration (testelchin.com.conf)

- Cache-Control: public, max-age=3600 — HTML pages
- Cache-Control: public, max-age=86400 — universe page
- Cache-Control: public, max-age=604800 — static assets (jpg, png, css, js)
- Security headers: X-Frame-Options, X-Content-Type-Options, HSTS, X-Served-By
- Rate limiting: 10 requests/second per IP, burst 20
- Custom error pages: 404, 50x
- absolute_redirect off — correct redirect behavior behind Traefik

## Site Structure

testelchin.com/                 — home page (Bezos quote)
testelchin.com/universe/        — galaxy background page
testelchin.com/dog.jpg          — test image
testelchin.com/universe/cat.jpg — test image in subdirectory

## Docker Image Versions

v1 - initial nginx deployment
v2 - custom HTML pages (home + universe with galaxy background)
v3 - nginx caching config added
v4 - fixed redirect + www support
v5 - production nginx config attempt (crashed — wrong config location)
v6 - fixed config location, full production config
v7 - added test images (dog.jpg, cat.jpg)
