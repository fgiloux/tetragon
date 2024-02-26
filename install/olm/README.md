# Deploying Tetragon with the Operator Lifecycle Manager (OLM)

This directory contains files for packaging the Tetragon Operator as an [OLM bundle](https://sdk.operatorframework.io/docs/olm-integration/tutorial-bundle/).
Such bundles can be published to a catalog and made available for installation and updates 
on Kubernetes clusters, where OLM is available. OLM comes preinstalled with OpenShift.

## Building and pushing an OLM bundle

Set the variables according to your environment:
```bash
export DOCKER_DEV_ACCOUNT=<your-account>
export DOCKER_IMAGE_TAG=latest
export DOCKER_REGISTRY=quay.io
```

And call the make targets at the root of the git repository:
```bash
make bundle-build bundle-push
```

## Deploying the bundle on a cluster

Prerequisites:
- OLM is available on the cluster
- The [operator-sdk CLI](https://sdk.operatorframework.io/docs/installation/) has been installed on your machine

```bash
kubectl create ns tetragon
operator-sdk run bundle  $DOCKER_REGISTRY/$DOCKER_DEV_ACCOUNT/tetragon-operator-bundle:$DOCKER_IMAGE_TAG -n tetragon
```

