.....

Thank you for taking the time to review this work. If you have any questions or would like to 
discuss the project further, please reach out at afoussom@gmail.com
.

API Gateway GitOps Project (Argo CD + Kubernetes)
Overview

This project demonstrates how to expose multiple Kubernetes applications using the Gateway API, 
managed declaratively through GitOps with Argo CD.
The repository is designed to reflect real-world production practices and is suitable for 
technical interviews, demos, and platform engineering reviews.



Architecture Summary

Traffic flow:

Internet
   ↓
Gateway (single entry point)
   ↓
HTTPRoute (path-based routing)
   ↓
Kubernetes Service
   ↓
Pods (Nginx applications)

Components
1. Applications

app1 – Nginx-based web application

app2 – Nginx-based web application

Each application includes:

Deployment (Pods)

Service (internal load balancing)

2. Gateway API

GatewayClass: nginx

Gateway: Defines the external entry point

HTTPRoute:

/app1 → app1-svc

/app2 → app2-svc

The Gateway acts as the single ingress point for all external traffic.



3. GitOps with Argo CD

Argo CD continuously monitors this repository

Any change committed to Git is automatically reconciled into the Kubernetes cluster

Ensures:

Declarative infrastructure

Auditability

Easy rollback


4. Repository Structure


argo-api-gateway-project/
├── apps/
│   ├── app1-deployment.yaml
│   ├── app1-service.yaml
│   ├── app2-deployment.yaml
│   └── app2-service.yaml
├── gateway/
│   ├── gateway.yaml
│   └── httproute.yaml
└── README.md

5. Prerequisites

Kubernetes cluster (v1.26+ recommended)

Gateway API CRDs installed

NGINX Gateway Controller installed

Argo CD installed and running

kubectl and argocd CLI access



6. Deployment via Argo CD

The project is deployed using Argo CD Application pointing to this repository.

Example workflow:

Commit Kubernetes manifests to Git

Argo CD detects changes

Argo CD applies and syncs resources automatically

Gateway exposes applications externally



7. Testing Access

Depending on the environment, applications can be tested using:

LoadBalancer IP

NodePort

Port-forwarding 

Example:

curl http://<GATEWAY-IP>/app1
curl http://<GATEWAY-IP>/app2


8. What This Project Demonstrates

Kubernetes Gateway API fundamentals

Path-based routing using HTTPRoute

Clean GitOps repository structure

Argo CD continuous reconciliation

Production-style Kubernetes exposure patterns
