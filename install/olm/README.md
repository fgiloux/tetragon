# Deploying Tetragon with the Operator Lifecycle Manager (OLM)

This directory contains files for packaging the Tetragon Operator as an [OLM bundle](https://sdk.operatorframework.io/docs/olm-integration/tutorial-bundle/).
Such bundles can be published to a catalog and made available for installation and updates 
on Kubernetes clusters, where OLM is available. OLM comes preinstalled with OpenShift.

## Building and pushing an OLM bundle

```bash
docker build -f bundle.Dockerfile -tag <container-registry-address>/tetragon-bundle:v0.0.1 .
docker push <container-registry-address>/tetragon-bundle:v0.0.1
```

## Deploying the bundle on a cluster

Prerequisites:
- OLM is available on the cluster
- The [operator-sdk CLI](https://sdk.operatorframework.io/docs/installation/) has been installed on your machine

```bash
kubectl create ns tetration
operator-sdk run bundle  <container-registry-address>/tetragon-bundle:v0.0.1 -n tetragon
```

