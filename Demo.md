# Open Application Model, Rudr, and Bedrock

## What

* The [Open Application Model](https://oam.dev) (OAM) is spec that separates *developer* roles from infrastructure *operator* roles in a codified abstraction.

* [Rudr](https://github.com/oam-dev/rudr) is a concrete implementation OAM specifically for Kubernetes. OAM is not limited to Kubernetes.

## Why  

* The Kubernetes ecosystem is vast and wild. Application developers want to focus on this applications and business logic. The surrounding pieces that control policy, network, storage, replication, etc are really secondary.

* Rudr attempts to create new model that splits up Kubernetes primative controllers into things that a developer might be concerned with configuring versus a cluster owner.

## How

Rudr's model consists of:

1. __Components__ aka your Docker image based microservice (stateless and stateful)
2. __Traits__ aka properties and configuration around your Kubernetes applications. Rudr current has abstractions for ingress, scalers, and volumes.
3. __Application Configuration__ aka a manifest that maps your components to traits and allows any additional declarations of configuration.

[//]: # (## Demo)

[//]: # (## Direction of Kubernetes related to Bedrock)

[//]: # (## Artifacts)

## Further Information

* The [Rudr](https://github.com/oam-dev/rudr) repository has in depth documentation and concept description along with several examples

* The OAM [announcement](https://cloudblogs.microsoft.com/opensource/2019/10/16/announcing-open-application-model/) from Microsoft blog.