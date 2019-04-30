## Autonity-platform helm chart

[![Join the chat at https://gitter.im/clearmatics/autonity](https://badges.gitter.im/clearmatics/autonity.svg)](https://gitter.im/clearmatics/autonity?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


## Introduction

It is umbrella chart `autonity-platform` that include main `autonity` subchart for deploy a **private** [Autonity](https://www.autonity.io/) network onto a [Kubernetes](http://kubernetes.io) 
cluster using the [Helm](https://helm.sh) package manager. Also `autonity-platform` can deploy additional charts and connect services inside as one infrastructure.

Autonity is a generalization of the Ethereum protocol based on a fork of go-ethereum. [Autonity Documentation](https://docs.autonity.io)

## Quick start
1. Install [Kubernetes cluster](http://kubernetes.io). You can do it using one of this ways:
   - Install minimal local kubernetes cluster out of box [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) or:
   - Install [Amazon EKS](https://eksworkshop.com/prerequisites/self_paced/) or:
   - Install [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine/docs/quickstart)
1. Install packet manager for kubernetes using this [Helm installation guide](https://helm.sh/docs/using_helm/#installing-helm)
1. Configure helm to your cluster
   ```bash
   helm init
   ```
1. Download `autonity-helm` chart and dependencies:
   ```bash
   git clone https://github.com/clearmatics/autonity-helm.git
   cd autonity-helm
   helm dependency update
   ```
1. Deploy it
   ```bash
   helm install -n autonity ./
   ```
## Prerequisites

* Kubernetes 1.10
* Helm 2.13

## Subcharts

* [Autonity](helm-charts/autonity) - **private** Autonity network with set of validators and observers (Enabled by default)
* [Ethstats](helm-charts/ethstats) - Web-dashboard for monitoring Autonity network (Optional)
* [Prometheus](https://github.com/helm/charts/tree/master/stable/prometheus) - Metrics system

## Configure

- You can change number of validators or observers using helm cli-options like this:
   ```bash
   helm install -n autonity ./ --set autonity.validators=6,autonity.observers=2
   ```
- You can enable optional subcharts like:
   ```bash
   helm install -n autonity ./ --set global.ethstats.enabled=true
   ```
- Also you can change any variables in this file [./values.yaml](values.yaml) before installation

## Connect to autonity network
```bash
# Forward JSON-RPC validator-0 to localhost
kubectl port-forward svc/validator-0 8545:8545

# Example  JSON-RPC request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}' http://localhost:8545

```

## Delete
```bash
helm delete autonity --purge
```