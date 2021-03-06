# Restorecommerce Helm Charts

This repository contains helm charts for the following services:

* [access-control-srv](./charts/access-control-srv)
* [catalog-srv](./charts/catalog-srv)
* [console](./charts/console)
* [fulfillment-srv](./charts/fulfillment-srv)
* [identity-srv](./charts/identity-srv)
* [indexing-srv](./charts/indexing-srv)
* [invoicing-srv](./charts/invoicing-srv)
* [notification-srv](./charts/notification-srv)
* [ordering-srv](./charts/ordering-srv)
* [ostorage-srv](./charts/ostorage-srv)
* [payment-srv](./charts/payment-srv)
* [pdf-rendering-srv](./charts/pdf-rendering-srv)
* [rendering-srv](./charts/rendering-srv)
* [scheduling-srv](./charts/scheduling-srv)
* [store-front](./charts/store-front)
* [system](./charts/system)

## Installation

You can install this helm repository via

```bash
helm repo add restorecommerce https://restorecommerce.github.io/helm/
helm repo update
```

## Example Deployment

There is an example deployment with all required dependencies specified in [example](./example) directory.

It uses the [helmfile](https://github.com/roboll/helmfile) tool to specify all releases and their values.

## Development

### Pre-Commit

There is a convenience script to execute all dev scripts in order:

```bash
./pre-commit.sh
```

If you wish to execute each step manually, they are described below:

### Linting

Linting uses the [chart-testing](https://github.com/helm/chart-testing) tool

```bash
ct lint --all --config .github/ct.yaml 
```

### Documentation Generation

Documentation generation uses the [helm-docs](https://github.com/norwoodj/helm-docs) tool

```bash
helm-docs
```

### Chart Validation

Validation uses the [kubeval](https://github.com/instrumenta/kubeval) tool

```bash
KUBERNETES_VERSION=1.19.2 ./.github/kubeval.sh
```

### Update Dependencies and Lockfiles

```bash
for CHART_DIR in ./charts/*; do
  helm dependency update "${CHART_DIR}"
done
```

## Packaging and Releasing

Packaging uses the [helm](https://helm.sh/) tool

Releasing uses the [chart-releaser](https://github.com/helm/chart-releaser) tool

Both tasks are executed by CI/CD when a branch is merged into master