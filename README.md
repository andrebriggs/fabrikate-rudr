# Fabrikate Rudr

A Fabrikate defintion to install [Rudr](https://github.com/oam-dev/rudr) on a Kubernetes cluster

## Ingress Controller

* nginx

## HorizontalPodAutoscaler Controller

* keda

## Uninstalling

To delete CRDs and associated Kubernetes objects run the following

```bash
kubectl delete crd -l app.kubernetes.io/part-of=core.oam.dev
```
