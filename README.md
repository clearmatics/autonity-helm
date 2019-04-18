## Autonity helm chart

[![Join the chat at https://gitter.im/clearmatics/autonity](https://badges.gitter.im/clearmatics/autonity.svg)](https://gitter.im/clearmatics/autonity?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Autonity is a generalization of the Ethereum protocol based on a fork of go-ethereum.

[Autonity Documentation](https://docs.autonity.io)

## Introduction

This chart deploys a **private** [Autonity](https://www.autonity.io/) network onto a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager. This chart is comprised of 4 components:

1. *initial jobs* that implement bootstrapping algorithm
1. *validators*: nodes that implement [IBFT consensus algorithms](https://docs.autonity.io/IBFT/index.html) [Source](https://github.com/clearmatics/autonity/blob/master/Dockerfile)
1. *observer*: node that connected with another validators by p2p and expose JSON-RPC and WebSocket interface [Source](https://github.com/clearmatics/autonity/blob/master/Dockerfile)
1. *ethstats*: [Ethereum Network Stats](https://github.com/cubedro/eth-netstats)

## Data storages

1. secret `account-pwd` contain generated account password.
1. secret `validators` or `observers` contain:   
   1. `0.private_key` - private key for account
1. configmap `validators` or `observers` contain:
   1. `0.address` - address
   1. `0.pub_key` - public key

## Prerequisites

* Kubernetes 1.10
* Helm 2.13


## Install

```console
$ git clone https://github.com/clearmatics/autonity-helm.git
$ helm install ./autonity-helm
```

## Connect to autonity network
```bash
# Forward JSON-RPC validator-0 to localhost
kubectl port-forward svc/validator-0 8545:8545

# Example  JSON-RPC request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}' http://localhost:8545

```
