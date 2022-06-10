# renovate

![Version: 32.38.0-bb.0](https://img.shields.io/badge/Version-32.38.0--bb.0-informational?style=flat-square) ![AppVersion: 32.38.0](https://img.shields.io/badge/AppVersion-32.38.0-informational?style=flat-square)

Universal dependency update tool that fits into your workflows.

## Upstream References
* <https://github.com/renovatebot/renovate>

* <https://github.com/renovatebot/renovate>
* <https://github.com/renovatebot/helm-charts>

## Learn More
* [Application Overview](docs/overview.md)
* [Other Documentation](docs/)

## Pre-Requisites

* Kubernetes Cluster deployed
* Kubernetes config installed in `~/.kube/config`
* Helm installed

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

* Clone down the repository
* cd into directory
```bash
helm install renovate chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| cronjob.schedule | string | `"0 1 * * *"` |  |
| cronjob.suspend | bool | `false` | If it is set to true, all subsequent executions are suspended. This setting does not apply to already started executions. |
| cronjob.annotations | object | `{}` |  |
| cronjob.labels | object | `{}` |  |
| cronjob.concurrencyPolicy | string | `""` |  |
| cronjob.failedJobsHistoryLimit | string | `""` |  |
| cronjob.successfulJobsHistoryLimit | string | `""` |  |
| cronjob.jobRestartPolicy | string | `"Never"` |  |
| cronjob.jobBackoffLimit | string | `""` |  |
| cronjob.startingDeadlineSeconds | string | `""` |  |
| pod.annotations | object | `{}` |  |
| pod.labels | object | `{}` |  |
| image.repository | string | `"registry1.dso.mil/ironbank/container-hardening-tools/renovate/renovate"` |  |
| image.tag | string | `"32.38.0"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| imagePullSecrets[0].name | string | `"private-registry"` |  |
| renovate.existingConfigFile | string | `""` | Custom exiting global renovate config |
| renovate.config | string | `""` | Inline global renovate config.json |
| ssh_config.enabled | bool | `false` |  |
| ssh_config.id_rsa | string | `""` |  |
| ssh_config.id_rsa_pub | string | `""` |  |
| ssh_config.config | string | `""` |  |
| ssh_config.existingSecret | string | `""` |  |
| secrets | object | `{}` |  |
| existingSecret | string | `""` |  |
| dind.enabled | bool | `false` | dind is non-functional in BB as it requires a privileged non-hardened container, changing this value does nothing |
| extraConfigmaps | list | `[]` | Additional configmaps. A generated configMap name is: "renovate.fullname" + "extra" + name(below) e.g. renovate-netrc-config |
| extraVolumes | list | `[]` | Additional volumes to the pod |
| extraVolumeMounts | list | `[]` | Additional volumeMounts to the container |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.name | string | `""` |  |
| resources | object | `{}` |  |
| envFrom | list | `[]` |  |
| env | object | `{}` |  |
| redis.enabled | bool | `false` | Enable the Redis subchart? |
| redis.architecture | string | `"standalone"` | Disable replication by default |
| redis.auth.enabled | bool | `false` | Don't require a password by default |
| redis.kubeVersion | string | `""` | Override Kubernetes version for redis chart |
| apiVersionOverrides.cronjob | string | `""` | String to override apiVersion of cronjob rendered by this helm chart |
| domain | string | `"bigbang.dev"` | Big Bang Values |
| istio.enabled | bool | `false` |  |
| istio.mtls.mode | string | `"PERMISSIVE"` | STRICT = Allow only mutual TLS traffic, PERMISSIVE = Allow both plain text and mutual TLS traffic PERMISSIVE is required for any action which redeploys pods because STRICT interferes with initContainers Can be changed to STRICT after all initContainers have finished but will interfere with upgrades/pod deployments that have initContainers |
| istio.renovate.enabled | bool | `true` |  |
| istio.renovate.gateways[0] | string | `"istio-system/public"` |  |
| networkPolicies.enabled | bool | `false` |  |
| networkPolicies.ingressLabels.app | string | `"istio-ingressgateway"` |  |
| networkPolicies.ingressLabels.istio | string | `"ingressgateway"` |  |
| networkPolicies.renovateTargetIpRange | string | `""` | IP range of target deployment |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
