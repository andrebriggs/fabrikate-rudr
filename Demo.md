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

## Why this is relevant to Bedrock work

OAM and Rudr are interesting because they follow they natural evolutions of all industries,  working towards abstracts for what was once complicated.

Talking about Kubernetes specifically, many agree that it is still quite difficult to get up and going. In the real world organizations are usually built around the idea of someone doing the "work" and someone else "managing" or overseeing the expected work. Checks and balances. Expecting an industry of developers and IT professionals to yield to the whims of a Kubernetes architecture is naive.

IMHO, Bedrock is about recognizing patterns that folks encounter when attempting to be productive with Kubernetes and _bundling_ the patterns that are reusable such as GitOps, IaC, deployment models such as canaries and blue/green. In addition observablity bundles such as an ELK stack.

The next evolution of that should allow anyone with any infrastructure (local, cloud, low resource/latency) to be productive in the simplest case by just focusing on their business logic. How can we bundle Kubernetes as a shiny appliance with big easy to see buttons and knobs that fulfill the use cases of _most_ organizations? There will always be situtations where the hood of the car needs to be popped open to hot rod the vechicle. We are not interested in that.

Taking building blocks and creating recognizable utilities. OAM is congruent with that mode of thinking. Other projects such as SMI and Dapr are also working in this direction.

[//]: # (## Artifacts)

## Further Information

* The [Rudr](https://github.com/oam-dev/rudr) repository has in depth documentation and concept description along with several examples

* The OAM [announcement](https://cloudblogs.microsoft.com/opensource/2019/10/16/announcing-open-application-model/) from Microsoft blog.