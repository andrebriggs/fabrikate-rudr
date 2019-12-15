# Fabrikate Rudr

* A Fabrikate defintion to install [Rudr](https://github.com/oam-dev/rudr) on a Kubernetes cluster
* This sample also configures a Docker image for [spartan-app](https://github.com/andrebriggs/spartan-app) to be deployed in the Rudr context.

## Install

1. Download the latest version of [Fabrikate](https://github.com/Microsoft/fabrikate).

2. Run the commands from the root of this repository

    ```bash
    $ fab install
    # Installs helm charts 
    $ fab generate
    # Generates manifests in ./generated/common
    $ kubectl apply -f ./generated/common
    # Apply Kubernetes manifests to your cluster
    ```

__Note__: You may have to run `kubectl apply` twice to ensure CRDs are installed.

## Ingress Controller

* nginx

## HorizontalPodAutoscaler Controller

* keda

## Uninstalling

To delete CRDs and associated Kubernetes objects run the following

```bash
kubectl delete crd -l app.kubernetes.io/part-of=core.oam.dev
```
