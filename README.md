## Autonity helm chart

[![Join the chat at https://gitter.im/clearmatics/autonity](https://badges.gitter.im/clearmatics/autonity.svg)](https://gitter.im/clearmatics/autonity?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Autonity is a generalization of the Ethereum protocol based on a fork of go-ethereum.

[Autonity Documentation](https://docs.autonity.io)

## Introduction

This chart deploys a **private** [Autonity](https://www.autonity.io/) network onto a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager. This chart is comprised of 4 components:

1. *NFS-server* as a persistent storage
1. *initial jobs* that implement bootstrapping algorithm
1. *validators*: nodes that implement [IBFT consensus algorithms](https://docs.autonity.io/IBFT/index.html) [Source](https://github.com/clearmatics/autonity/blob/master/Dockerfile)
1. *observer*: node that connected with another validators by p2p and expose JSON-RPC and WebSocket interface [Source](https://github.com/clearmatics/autonity/blob/master/Dockerfile)
1. *ethstats*: [Ethereum Network Stats](https://github.com/cubedro/eth-netstats)

## Prerequisites

* Kubernetes 1.11
* Helm 2.13


## Install

```console
$ git clone https://github.com/clearmatics/autonity-helm.git
$ helm install ./autonity-helm
```

