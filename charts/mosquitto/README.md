# Mosquitto

This chart installs [Mosquitto](https://mosquitto.org/), an open source (EPL/EDL licensed) message broker that implements the MQTT protocol versions 5.0, 3.1.1 and 3.1. Mosquitto is lightweight and is suitable for use on all devices from low power single board computers to full servers.

## TL;DR;

```bash
$ helm repo add naps https://naps.github.io/helm-charts/
$ helm install my-release naps/mosquitto
```

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install my-release naps/mosquitto
```

The command deploys Mosquitto on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.


## Parameters

The following table lists the configurable parameters of the Redis chart and their default values.

| Parameter                                   | Description                                                                                            | Default             |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------- |
| `replicaCount`                              | Number of Mosquitto Pods to run                                                                        | `1`                 |
| `image.repository`                          | Mosquitto image                                                                                        | `eclipse-mosquitto` |
| `image.pullPolicy`                          | Mosquitto image pull policy                                                                            | `IfNotPresent`      |
| `imagePullSecrets`                          | Docker-registry secret names as an array                                                               | `[]`                |
| `nameOverride`                              | String to partially override mosquitto.fullname template with a string (will prepend the release name) | `""`                |
| `fullnameOverride`                          | String to fully override mosquitto.fullname template with a string                                     | `""`                |
| `podSecurityContext`                        | Security context (Pod wide)                                                                            | `{}`                |
| `securityContext`                           | Security context (Mosquitto container wide)                                                            | `{}`                |
| `service.type`                              | Kubernetes Service type                                                                                | `ClusterIP`         |
| `service.ports.mqtt`                        | Port to use for MQTT protocol                                                                          | `1883`              |
| `service.ports.mqttssl`                     | Port to use for MQTT over SSL protocol                                                                 | `8883`              |
| `service.ports.mqttws`                      | Port to use for MQTT over WebSocket protocol                                                           | `9001`              |
| `resources`                                 | Mosquitto CPU/Memory resource requests/limits                                                          | `{}`                |
| `nodeSelector`                              | Mosquitto labels for pod assignment                                                                    | `{}`                |
| `tolerations`                               | Toleration labels for Mosquitto pod assignment                                                         | `[]`                |
| `affinity`                                  | Affinity settings for Mosquitto pod assignment                                                         | `{}`                |
| `mosquitto.config`                          | Extra configuration to be appended to the Mosquitto configuration                                      | `""`                |
| `mosquitto.users`                           | Mosquitto users configuration                                                                          | `""`                |
| `mosquitto.acls`                            | Mosquitto ACLs configuration                                                                           | `""`                |
| `mosquitto.ssl.enabled`                     | Enable the SSL socket on Mosquitto                                                                     | `false`             |
| `mosquitto.ssl.portName`                    | Port name (in Service ports) to use for SSL                                                            | `mqttssl`           |
| `mosquitto.ssl.secretName`                  | Secret name to use to retrieve the SSL certificate                                                     | `mosquitto-ssl`     |
| `mosquitto.ssl.certificate.enabled`         | Enable the Certificate resources (cert-manager integration)                                            | `false`             |
| `mosquitto.ssl.certificate.dnsNames`        | Certificate DNS names                                                                                  | `[]`                |
| `mosquitto.ssl.certificate.issuerRef.group` | Certificate issuer group to use                                                                        | `cert-manager.io`   |
| `mosquitto.ssl.certificate.issuerRef.kind`  | Certificate issuer kind to use                                                                         | `ClusterIssuer`     |
| `mosquitto.ssl.certificate.issuerRef.name`  | Certificate issuer name to use                                                                         | `letsencrypt`       |
| `mosquitto.persistence.enabled`             | Enable Mosquitto persistency                                                                           | `false`             |
| `mosquitto.persistence.path`                | Path to mount the volume at, to use other images                                                       | `/mosquitto/data`   |
| `mosquitto.persistence.subPath`             | Subdirectory of the volume to mount at                                                                 | `""`                |
| `mosquitto.persistence.existingClaim`       | Use an existing PVC to persist data                                                                    | `""`                |
| `mosquitto.persistence.storageClass`        | Storage class of backing PVC                                                                           | see values.yaml     |
| `mosquitto.persistence.accessModes`         | Persistent Volume Access Modes                                                                         | `["ReadWriteOnce"]` |
| `mosquitto.persistence.size`                | Size of data volume                                                                                    | `1Gi`               |
| `mosquitto.persistence.matchLabels`         | matchLabels persistent volume selector                                                                 | `{}`                |
| `mosquitto.persistence.matchExpressions`    | matchExpressions persistent volume selector                                                            | `{}`                |


























## Configuration
<!-- this section is optional if there is nothing special about your config --> 

### Secrets

The following secrets are configurable:

- username
- password

### Labels

You can use the following labels for maximum fun.

- lol=cat

### Environment Variables

The foo pods also have the following environment variables:

- getfired
 - false: does something totally reasonable.
 - true: close your laptop and walk out.

## Usage

Once installed, you can access the application by (hitting a url | executing a command) as follows:

```console
export NODEPORT=`kubectl get svc --selector='app=foo,heritage=helm' --output=template --template="{{ with index .items 0}}{{with index .spec.ports 0 }}{{.nodePort}}{{end}}{{end}}"`
export NODE=`kubectl get nodes --output=template --template="{{with index .items 0 }}{{.metadata.name}}{{end}}"`

curl http://$NODE:$NODEPORT
```
--or--

```console 
export PODNAME=`kubectl get pod --selector='app=foo,heritage=helm' --output=template --template="{{with index .items 0}}{{.metadata.name}}{{end}}"

kubectl exec $PODNAME command
```

The foo pods can also be scaled:

```console
kubectl scale rc foo --replicas=10
```

## More Info

The Baz Foundation is the best resource for all things Foo:

http://baz.org