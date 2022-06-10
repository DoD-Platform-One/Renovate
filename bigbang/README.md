# Big Bang compatible Helm chart

This helm chart deploys the application using the same methods and values as Big Bang.

## Prerequisites

- Kubernetes cluster matching [Big Bang's Prerequisites](https://repo1.dso.mil/platform-one/big-bang/bigbang/-/tree/master/docs/guides/prerequisites)
- [FluxCD](https://fluxcd.io/) running in the cluster
- The [Big Bang git repository](https://repo1.dso.mil/platform-one/big-bang/bigbang) cloned into `~/bigbang`
- [Helm](https://helm.sh/docs/intro/install/)

## Usage

### Installation

1. Install Big Bang

```helm upgrade -i -n bigbang --create-namespace -f ~/bigbang/chart/values.yaml -f bigbang/values.yaml bigbang ~/bigbang/chart```

2. Install this chart

```helm upgrade -i -n bigbang --create-namespace -f ~/bigbang/chart/values.yaml -f bigbang/values.yaml bigbang-renovate bigbang```

### Removal

```helm delete -n bigbang bigbang-renovate```

