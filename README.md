## Deployment ##

GitOps‑based Kubernetes deployment repository for the hello-app service, managed via ArgoCD.
This repository contains both the Kubernetes manifests for the application and the ArgoCD Application definition responsible for deploying it into an EKS cluster.

## Repository Structure ##

```
cp-interview-deployments/
│
├── apps/
│   └── stage/
│       └── hello-app/
│           ├── deployment.yaml
│           ├── ingress-class.yaml
│           ├── ingress.yaml
│           └── service.yaml
│
├── controller/
│   └── stage/
│       └── hello-app.yaml   # ArgoCD Application manifest
│
|── infra.yaml
|── stage.yaml
└── README.md
```

## apps/stage/hello-app/ ##

Contains the Kubernetes manifests for deploying the hello-app service into the stage environment:

deployment.yaml — Pod and ReplicaSet definition for the hello-app container
service.yaml — ClusterIP/LoadBalancer service exposing the app
ingress.yaml — Ingress routing configuration
ingress-class.yaml — Custom ingress class definition

## controller/stage/hello-app.yaml ##

ArgoCD Application manifest that defines:

Which path in the repo to watch
Which cluster to deploy to
Which namespace to create/use
Automated sync, pruning, and self-healing policies

## stage.yaml

ArgoCD Application manifest that defines:

All the application that related to stage environment

## How to Deploy ##
```
kubectl apply -f stage.yaml
```

## Access to application
Curl command you need to hit the Kubernetes Ingress endpoint while overriding the Host header
client -> ALB -> Ingress -> service -> pod

```
curl -H "Host: hello-world.cp-interview.com" http://k8s-helloapp-hellonod-a624d878d7-809775282.us-east-2.elb.amazonaws.com
```

# Crossplan deployment #
Argocd application infra provision vpc resources
- vpc
- subnets
- internetGateway
- routetable

## Contributors: ##
noy5277@gmail.com