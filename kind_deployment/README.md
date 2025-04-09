# Deployment-Flux-Main
## Overview
The "Deployment-Flux-Main" repository is designed to facilitate the automated deployment and management of applications in Kubernetes clusters using Flux CD. This repository contains configuration files and scripts for setting up Kubernetes (k8s) clusters in different environments (e.g., local and Azure) and deploying applications to them through Flux CD.

## Purpose
The primary purpose of this repository is to:

* Automate the creation of Kubernetes clusters using kind (Kubernetes IN Docker), which allows running Kubernetes clusters within Docker containers.
Utilize Flux CD to automate the deployment of applications to these Kubernetes clusters based on the configurations stored in the repository.
* Support multiple environments (e.g., single environment, staging, production) to ensure that applications can be deployed and managed across different stages of the development lifecycle.
## Features
* Multi-Node Cluster Creation: Scripts and configurations for creating multi-node Kubernetes clusters using kind. This is suitable for simulating more realistic environments compared to single-node clusters.
Flux CD Bootstrapping: Commands and configurations for bootstrapping Flux CD on the created Kubernetes clusters. This sets up Flux CD to automatically apply changes from specified paths in the repository to the corresponding clusters.
* Environment-Specific Deployments: Support for deploying to different environments (e.g., single environment, staging, production) by specifying different configurations and paths for Flux CD.
## How It Works
* Create Kubernetes Clusters: The repository contains YAML configuration files for creating multi-node Kubernetes clusters for different environments using kind. This step involves executing commands to create clusters named staging and production, each with its own configuration.

* Bootstrap Flux CD: After the clusters are created, Flux CD is bootstrapped on each cluster. This involves specifying the GitHub repository details, branch, path for the configurations, and marking the repository as personal. Flux CD then monitors these paths for changes and applies them to the clusters.

* Deploy Applications: With Flux CD set up, applications can be deployed to the Kubernetes clusters by adding or updating their configurations in the specified paths within the repository. Flux CD automatically picks up these changes and applies them to the clusters.
## Create Kind Cluster. Multi-Node

#### Single Env Deployment
kind create cluster --config=./kind_deployment/kind-multi-node.yaml

flux bootstrap github --owner=airkine --repository=deployment-flux-main --branch=main --path=./clusters/kind/eastus2 --personal

## Deploy source podinfo (Gitrepository source)

`flux create source git podinfo \
  --url=https://github.com/stefanprodan/podinfo \
  --branch=master \
  --interval=1m \
  --export > ./clusters/kind/podinfo-source.yaml`

`git add -A && git commit -m "Add podinfo GitRepository"`
`git push`

## Deploy application podinfo

`kubectl create ns podinfo`

`flux create kustomization podinfo \
  --target-namespace=podinfo \
  --source=podinfo \
  --path="./kustomize" \
  --prune=true \
  --wait=true \
  --interval=30m \
  --retry-interval=2m \
  --health-check-timeout=3m \
  --export > ./clusters/kind/podinfo-kustomization.yaml`

## Commands for Troubleshooting
###### Find repos flux is monitoring
`kubectl get gitrepo -n flux-system`

###### Force reconciliation
`flux reconcile kustomization flux-system --with-source`
