# Grav

[Grav](https://getgrav.org/) Build Faster Websites
Grav is a modern open source flat-file CMS


## This Helm chart

Given the personal helm chart of Grav at [bitnami/charts](https://github.com/magikcypress/helm-grav).


```bash
$ git clone https://github.com/magikcypress/helm-grav.git
$ helm install my-release helm-grav           # Helm 3
$ helm install --name my-release helm-grav    # Helm 2
```

To update an exisiting deployment with a chart hosted in this repository you can execute

```bash
$ git pull 
$ helm upgrade my-release helm-grav
```

## TL;DR;

```console
helm install my-release helm-grav
```

## Introduction

This chart bootstraps [Grav](https://github.com/magikcypress/docker-grav-arm) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

This package propose a chart for docker ARM for Kubernetes Cluster on Raspberry PI.

## Prerequisites

- Kubernetes 1.12+
- Helm 2.11+ or Helm 3.0-beta3+
- PV provisioner support in the underlying infrastructure
- ReadWriteMany volumes for deployment scaling

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install my-release helm-grav
```

The command deploys grav on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the grav chart and their default values per section/component:

### Global parameters

| Parameter                 | Description                                     | Default                                                 |
|---------------------------|-------------------------------------------------|---------------------------------------------------------|
| `global.imageRegistry`    | Global Docker image registry                    | `nil`                                                   |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`     | Global storage class for dynamic provisioning   | `nil`                                                   |

### Common parameters

| Parameter                 | Description                                     | Default                                                 |
|---------------------------|-------------------------------------------------|---------------------------------------------------------|
| `nameOverride`            | String to partially override grav.fullname | `nil`                                                   |
| `fullnameOverride`        | String to fully override grav.fullname     | `nil`                                                   |
| `clusterDomain`           | Default Kubernetes cluster domain               | `cluster.local`                                         |

### Grav parameters

| Parameter                            | Description                                                                   | Default                                                 |
|--------------------------------------|-------------------------------------------------------------------------------|---------------------------------------------------------|
| `image.registry`                     | grav image registry                                                      | `docker.io`                                             |
| `image.repository`                   | grav image name                                                          | `magikcypress/grav-arm:latest`                                     |
| `image.tag`                          | grav image tag                                                           | `{TAG_NAME}`                                            |
| `image.pullPolicy`                   | grav image pull policy                                                   | `IfNotPresent`                                          |
| `image.pullSecrets`                  | Specify docker-registry secret names as an array                              | `[]` (does not add image pull secrets to deployed pods) |
| `image.debug`                        | Specify if debug logs should be enabled                                       | `false`                                                 |
| `gravSkipInstall`               | Skip wizard installation                                                      | `false`                                                 |
| `gravUsername`                  | User of the application                                                       | `user`                                                  |
| `gravPassword`                  | Application password                                                          | _random 10 character long alphanumeric string_          |
| `gravEmail`                     | Admin email                                                                   | `user@example.com`                                      |
| `gravFirstName`                 | First name                                                                    | `FirstName`                                             |
| `gravLastName`                  | Last name                                                                     | `LastName`                                              |
| `gravBlogName`                  | Blog name                                                                     | `User's Blog!`                                          |
| `gravTablePrefix`               | Table prefix                                                                  | `wp_`                                                   |
| `gravScheme`                    | Scheme to generate application URLs [`http`, `https`]                         | `http`                                                  |
| `allowEmptyPassword`                 | Allow DB blank passwords                                                      | `true`                                                  |
| `allowOverrideNone`                  | Set Apache AllowOverride directive to None                                    | `false`                                                 |
| `customHTAccessCM`                   | Configmap with custom grav-htaccess.conf directives                      | `nil`                                                   |
| `smtpHost`                           | SMTP host                                                                     | `nil`                                                   |
| `smtpPort`                           | SMTP port                                                                     | `nil`                                                   |
| `smtpUser`                           | SMTP user                                                                     | `nil`                                                   |
| `smtpPassword`                       | SMTP password                                                                 | `nil`                                                   |
| `smtpUsername`                       | User name for SMTP emails                                                     | `nil`                                                   |
| `smtpProtocol`                       | SMTP protocol [`tls`, `ssl`, `none`]                                          | `nil`                                                   |
| `extraEnv`                           | Additional container environment variables                                    | `[]`                                                    |
| `extraVolumeMounts`                  | Additional volume mounts                                                      | `[]`                                                    |
| `extraVolumes`                       | Additional volumes                                                            | `[]`                                                    |
| `sidecars`                           | Attach additional sidecar containers to the pod                               | `nil`                                                   |
| `replicaCount`                       | Number of grav Pods to run                                               | `1`                                                     |
| `updateStrategy`                     | Set up update strategy                                                        | `RollingUpdate`                                         |
| `schedulerName`                      | Name of the alternate scheduler                                               | `nil`                                                   |
| `securityContext.enabled`            | Enable security context for grav pods                                    | `true`                                                  |
| `securityContext.fsGroup`            | Group ID for the grav filesystem                                         | `1001`                                                  |
| `securityContext.runAsUser`          | User ID for the grav container                                           | `1001`                                                  |
| `resources.limits`                   | The resources limits for the grav container                              | `{}`                                                    |
| `resources.requests`                 | The requested resources for the grav container                           | `{"memory": "512Mi", "cpu": "300m"}`                    |
| `nodeSelector`                       | Node labels for pod assignment                                                | `{}` (evaluated as a template)                          |
| `tolerations`                        | Tolerations for pod assignment                                                | `[]` (evaluated as a template)                          |
| `affinity`                           | Affinity for pod assignment                                                   | `{}` (evaluated as a template)                          |
| `podAnnotations`                     | Pod annotations                                                               | `{}` (evaluated as a template)                          |
| `healthcheckHttps`                   | Use https for liveliness and readiness                                        | `false`                                                 |
| `livenessProbe.enabled`              | Enable/disable livenessProbe                                                  | `true`                                                  |
| `livenessProbe.initialDelaySeconds`  | Delay before liveness probe is initiated                                      | `120`                                                   |
| `livenessProbe.periodSeconds`        | How often to perform the probe                                                | `10`                                                    |
| `livenessProbe.timeoutSeconds`       | When the probe times out                                                      | `5`                                                     |
| `livenessProbe.failureThreshold`     | Minimum consecutive failures for the probe                                    | `6`                                                     |
| `livenessProbe.successThreshold`     | Minimum consecutive successes for the probe                                   | `1`                                                     |
| `livenessProbeHeaders`               | Headers to use for livenessProbe                                              | `{}`                                                    |
| `readinessProbe.enabled`             | Enable/disable readinessProbe                                                 | `true`                                                  |
| `readinessProbe.initialDelaySeconds` | Delay before readiness probe is initiated                                     | `30`                                                    |
| `readinessProbe.periodSeconds`       | How often to perform the probe                                                | `10`                                                    |
| `readinessProbe.timeoutSeconds`      | When the probe times out                                                      | `5`                                                     |
| `readinessProbe.failureThreshold`    | Minimum consecutive failures for the probe                                    | `6`                                                     |
| `readinessProbe.successThreshold`    | Minimum consecutive successes for the probe                                   | `1`                                                     |
| `readinessProbeHeaders`              | Headers to use for readinessProbe                                             | `{}`                                                    |
| `service.annotations`                | Service annotations                                                           | `{}` (evaluated as a template)                          |
| `service.type`                       | Kubernetes Service type                                                       | `LoadBalancer`                                          |
| `service.port`                       | Service HTTP port                                                             | `80`                                                    |
| `service.httpsPort`                  | Service HTTPS port                                                            | `443`                                                   |
| `service.httpsTargetPort`            | Service Target HTTPS port                                                     | `https`                                                 |
| `service.loadBalancerSourceRanges`   | Restricts access for LoadBalancer (only with `service.type: LoadBalancer`)    | `[]`                                                    |
| `service.metricsPort`                | Service Metrics port                                                          | `9117`                                                  |
| `service.externalTrafficPolicy`      | Enable client source IP preservation                                          | `Cluster`                                               |
| `service.nodePorts.http`             | Kubernetes http node port                                                     | `""`                                                    |
| `service.nodePorts.https`            | Kubernetes https node port                                                    | `""`                                                    |
| `service.nodePorts.metrics`          | Kubernetes metrics node port                                                  | `""`                                                    |
| `service.extraPorts`                 | Extra ports to expose in the service (normally used with the `sidecar` value) | `nil`                                                   |
| `persistence.enabled`                | Enable persistence using PVC                                                  | `true`                                                  |
| `persistence.existingClaim`          | Enable persistence using an existing PVC                                      | `nil`                                                   |
| `persistence.storageClass`           | PVC Storage Class                                                             | `nil` (uses alpha storage class annotation)             |
| `persistence.accessMode`             | PVC Access Mode                                                               | `ReadWriteOnce`                                         |
| `persistence.size`                   | PVC Storage Request                                                           | `10Gi`                                                  |

### Ingress parameters

| Parameter                         | Description                                              | Default                        |
|-----------------------------------|----------------------------------------------------------|--------------------------------|
| `ingress.enabled`                 | Enable ingress controller resource                       | `false`                        |
| `ingress.certManager`             | Add annotations for cert-manager                         | `false`                        |
| `ingress.hostname`                | Default host for the ingress resource                    | `grav.local`              |
| `ingress.annotations`             | Ingress annotations                                      | `[]` (evaluated as a template) |
| `ingress.extraHosts[0].name`      | Additional hostnames to be covered                       | `nil`                          |
| `ingress.extraHosts[0].path`      | Additional hostnames to be covered                       | `nil`                          |
| `ingress.extraTls[0].hosts[0]`    | TLS configuration for additional hostnames to be covered | `nil`                          |
| `ingress.extraTls[0].secretName`  | TLS configuration for additional hostnames to be covered | `nil`                          |
| `ingress.secrets[0].name`         | TLS Secret Name                                          | `nil`                          |
| `ingress.secrets[0].certificate`  | TLS Secret Certificate                                   | `nil`                          |
| `ingress.secrets[0].key`          | TLS Secret Key                                           | `nil`                          |                                     |

### Metrics parameters

| Parameter                                 | Description                                                                  | Default                                                      |
|-------------------------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------|
| `metrics.enabled`                         | Start a side-car prometheus exporter                                         | `false`                                                      |
| `metrics.image.registry`                  | Apache exporter image registry                                               | `docker.io`                                                  |
| `metrics.image.repository`                | Apache exporter image name                                                   | `bitnami/apache-exporter`                                    |
| `metrics.image.tag`                       | Apache exporter image tag                                                    | `{TAG_NAME}`                                                 |
| `metrics.image.pullPolicy`                | Image pull policy                                                            | `IfNotPresent`                                               |
| `metrics.image.pullSecrets`               | Specify docker-registry secret names as an array                             | `[]` (does not add image pull secrets to deployed pods)      |
| `metrics.podAnnotations`                  | Additional annotations for Metrics exporter pod                              | `{prometheus.io/scrape: "true", prometheus.io/port: "9117"}` |
| `metrics.resources.limits`                | The resources limits for the metrics exporter container                      | `{}`                                                         |
| `metrics.resources.requests`              | The requested resources for the metrics exporter container                   | `{}`                                                         |
| `metrics.serviceMonitor.enabled`          | Create ServiceMonitor Resource for scraping metrics using PrometheusOperator | `false`                                                      |
| `metrics.serviceMonitor.namespace`        | Namespace where servicemonitor resource should be created                    | `nil`                                                        |
| `metrics.serviceMonitor.interval`         | Specify the interval at which metrics should be scraped                      | `30s`                                                        |
| `metrics.serviceMonitor.scrapeTimeout`    | Specify the timeout after which the scrape is ended                          | `nil`                                                        |
| `metrics.serviceMonitor.relabellings`     | Specify Metric Relabellings to add to the scrape endpoint                    | `nil`                                                        |
| `metrics.serviceMonitor.honorLabels`      | honorLabels chooses the metric's labels on collisions with target labels.    | `false`                                                      |
| `metrics.serviceMonitor.additionalLabels` | Used to pass Labels that are required by the Installed Prometheus Operator   | `{}`                                                         |

The above parameters map to the env variables defined in [magikcypress/docker-grav-arm](http://github.com/magikcypress/docker-grav-arm). For more information please refer to the [magikcypress/docker-grav-arm](http://github.com/magikcypress/docker-grav-arm) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install my-release \
  --set gravUsername=admin \
  --set gravPassword=password \
    helm-grav
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install my-release -f values.yaml helm-grav
```

> **Tip**: You can use the default [values.yaml](values.yaml)
