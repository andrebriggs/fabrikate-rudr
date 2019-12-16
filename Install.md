# Installing Fabrikate Rudr

* A Fabrikate defintion to install [Rudr](https://github.com/oam-dev/rudr) on a Kubernetes cluster
* This sample also configures a Docker image for [spartan-app](https://github.com/andrebriggs/spartan-app) to be deployed in the Rudr context.
* Nginx is installed as your *Ingress* and Keda is used as the *HorizontalPodAutoscaler*

## Install

1. Download the latest version of [Fabrikate](https://github.com/Microsoft/fabrikate).

2. Ensure your Kubernetes cluster is version 1.15 or above. 

3. Run the commands from the root of this repository

    ```bash
    $ fab install
    # Installs helm charts 
    $ fab generate
    # Generates manifests in ./generated/common
    $ kubectl apply -f ./generated/common
    # Apply Kubernetes manifests to your cluster
    ```

__Note__: You may have to run `kubectl apply` twice to ensure CRDs are installed.

## Verifying Application Deployment

After everything has been in installed you can reun the following commands to verify your ingress was configured

```bash
$ kubectl get ingress -o yaml
# See yaml with a label reference to your application configuration name
```

Verify components, configuration, and traits are installed.
```bash
$ kubectl get component,configuration,trait
NAME                                                 AGE
componentschematic.core.oam.dev/spartan-app-v1       37h

NAME                                              AGE
applicationconfiguration.core.oam.dev/first-app   24h

NAME                                AGE
trait.core.oam.dev/autoscaler       3d
trait.core.oam.dev/empty            3d
trait.core.oam.dev/ingress          3d
trait.core.oam.dev/manual-scaler    3d
trait.core.oam.dev/volume-mounter   3d
```

Find the external IP for your ingress controller
```bash
$ kubectl get svc
NAME                            TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
first-app-spartan-app-v1        ClusterIP      10.0.220.78    <none>           8080/TCP                     24h
healthscope                     ClusterIP      10.0.33.62     <none>           80/TCP                       3d
keda-operator                   ClusterIP      10.0.213.255   <none>           443/TCP,80/TCP               2d23h
keda-operator-metrics           ClusterIP      10.0.245.98    <none>           8383/TCP,8686/TCP            2d23h
kubernetes                      ClusterIP      10.0.0.1       <none>           443/TCP                      3d13h
nginx-ingress-controller        LoadBalancer   10.0.170.123   40.XXX.XXX.XXX   80:30387/TCP,443:30373/TCP   2d23h
nginx-ingress-default-backend   ClusterIP      10.0.185.62    <none>           80/TCP                       2d23h
```

Finally you can [visit](https://github.com/oam-dev/rudr/blob/d1a4d2ba3accdcab2700b22176d485633abde9b7/docs/tutorials/deploy_and_update.md#visit-the-web-app) the web app to verify. In this case we will use a slightly different syntax

```bash
$ export POD_NAME=$(kubectl get pods -l "oam.dev/instance-name=first-app-spartan-app-v1,app.kubernetes.io/name=first-app" -o jsonpath="{.items[0].metadata.name}")

$ kubectl port-forward $POD_NAME 8080:8080
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

In a separate shell session
```bash
$ curl localhost:8080
Hi! I'm instance 651 running version 0.1 of your application at 2019-12-16 20:31:39
```

## Concepts at play in this repo

Here we briefly describe what how the Rudr concepts are in action in this repo. Please read Rudr docs for more info.

### Rudr Components

We define one component in this sample. [This](manifest/rudr-component.yaml) hardcoded yaml file has a reference to the Docker image I wish to deploy. It also defines the workload type (a Rudr [concept](https://github.com/oam-dev/rudr/blob/master/docs/concepts/workloads.md)). Keep in mind this hardcoded yaml file could have been Helm templated too!

### Rudr Application Configuration

The configuration of our above component is defined in the [configuration](manifest/rudr-configuration.yaml) yaml file. Within here you see a reference to the component name _spartan-app-v1_ and an instance name of that component

### Rudr Traits

In the configuration file we also see a section for traits. The trait we are setting up is for ingress.

## Uninstalling

To delete CRDs and associated Kubernetes objects run the following

```bash
kubectl delete crd -l app.kubernetes.io/part-of=core.oam.dev
```
