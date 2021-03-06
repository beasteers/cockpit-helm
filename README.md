
Cockpit
===========

A Cockpit Helm chart for Kubernetes

Cockpit is a headless CMS with an API-first approach that puts content first. It is designed to simplify the process of publication by separating content management from content consumption on the client side.

Cockpit is focusing just on the back-end work to manage content. Rather than worry about delivery of content through pages, its goal is to provide structured content across different channels via a simple API.

Key features:
 - Manage flexible content models. There are no pre-defined content models. Define the content model yourself.
 - Uncluttered UI. Cockpit offers you a modern and simple user interface.
 - One system, consume it the way you want. Receive your content via a simple API.

The Advantages Of Going Headless
 - No presentation limitations – build the best design ever.
 - Content for multiple channels – create content once, consume anywhere.
 - Highly scalable content – for all your devices and microsites.
 - Minimum training required – get started, immediately.
 - Easy integrations – connect with everything.

## Installation
Temporary instructions:
```bash
# pull the chart
git clone https://github.com/beasteers/cockpit.git
git checkout k8s-helm

# overwrite with custom values (optional)
cp ./cockpit/charts/cockpit/values.yml ./cockpit.values.yml

helm install cockpit ./cockpit/charts/cockpit -f ./cockpit.values.yml
```
Eventually, we should have something like `helm repo add cockpit.github.io/helm`

## Uninstalling
```bash
helm uninstall cockpit
```

## TODO:
  - Add collection installation (either CRD or in values.yml)
  - Add form installation
  - Add singleton installation
  - Add webhook installation
I don't know if I really want to get into the complications of having to
do this in a CRD, so the easiest thing to do would be to have this in `values.yml`:
```
collections:
  somecollectionname:
    data:
      fields:
        - ...
```
do that for each asset type and write each to their own config map.

Then in the initContainer count the configmap, loop thru the files and post them to cockpit. maybe check that they already exist so you don't overwrite manual changes.

For collection update endpoints: https://getcockpit.com/documentation/api/collections

## Notes
To generate the README:
```bash
frigate gen --output-format markdown . > README.md
```

## Configuration

The following table lists the configurable parameters of the Cockpit chart and their default values.

| Parameter                | Description             | Default        |
| ------------------------ | ----------------------- | -------------- |
| `replicas` | The number of pod replicas | `1` |
| `image.repository` | Image repository | `"agentejo/cockpit"` |
| `image.pullPolicy` | Image pull policy | `"IfNotPresent"` |
| `image.tag` | Image tag. overrides the image tag whose default is the chart appversion. | `""` |
| `image.pullSecrets` | Image pull secrets | `[]` |
| `nameOverride` | Override the ... something | `""` |
| `fullnameOverride` | Override the pod/service/ingress names | `""` |
| `config` | Cockpit configuration options. see https://getcockpit.com/documentation/reference/configuration | `{}` |
| `languages` | Supported languages (use il8n code). source: https://github.com/agentejo/cockpit-i18n | `[]` |
| `extraEnv` | Extra environment variables. | `{}` |
| `service.type` | Kubernetes service type | `"ClusterIP"` |
| `service.port` | Kubernetes port where service is exposed | `80` |
| `ingress.enabled` | Enable ingress | `false` |
| `ingress.annotations` | Ingress annotations | `{}` |
| `ingress.hosts` | Ingress hosts | `[{"host": "chart-example.local", "paths": ["/"]}]` |
| `ingress.tls` | Ingress tls configuration | `[]` |
| `persistence.enabled` | Enable persistent storage | `false` |
| `persistence.storageClassName` | Type of volume claim | `""` |
| `persistence.size` | Size of volume claim | `"1Gi"` |
| `persistence.subPath` | Mount a sub dir of the persistent volume | `""` |
| `resources` | Define required node resources | `{}` |
| `serviceAccount.create` | Specifies whether a service account should be created | `true` |
| `serviceAccount.annotations` | Annotations to add to the service account | `{}` |
| `serviceAccount.name` | The name of the service account to use. if not set and create is true, a name is generated using the fullname template | `""` |
| `podAnnotations` | 	pod annotations | `{}` |
| `podSecurityContext` | Pod securitycontext | `{}` |
| `securityContext` | Statefulset securitycontext | `{}` |
| `autoscaling.enabled` | Enable autoscaling | `false` |
| `autoscaling.minReplicas` | Minimum number of autoscale replicas | `1` |
| `autoscaling.maxReplicas` | Maximum number of autoscale replicas | `100` |
| `autoscaling.targetCPUUtilizationPercentage` | Target cpu utilization | `80` |
| `nodeSelector` | Node labels for pod assignment | `{}` |
| `tolerations` | Toleration labels for pod assignment | `[]` |
| `affinity` | Affinity settings for pod assignment | `{}` |



---
_Documentation generated by [Frigate](https://frigate.readthedocs.io)._

