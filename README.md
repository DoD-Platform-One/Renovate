<!-- Warning: Do not manually edit this file. See notes on gluon + helm-docs at the end of this file for more information. -->
# renovate

![Version: 39.83.3-bb.0](https://img.shields.io/badge/Version-39.83.3--bb.0-informational?style=flat-square) ![AppVersion: 39.83.3](https://img.shields.io/badge/AppVersion-39.83.3-informational?style=flat-square) ![Maintenance Track: bb_integrated](https://img.shields.io/badge/Maintenance_Track-bb_integrated-green?style=flat-square)

Universal dependency update tool that fits into your workflows.

## Upstream References
- <https://github.com/renovatebot/renovate>
- <https://github.com/renovatebot/helm-charts>

## Upstream Release Notes

This package has no upstream release note links on file. Please add some to [chart/Chart.yaml](chart/Chart.yaml) under `annotations.bigbang.dev/upstreamReleaseNotesMarkdown`.
Example:
```yaml
annotations:
  bigbang.dev/upstreamReleaseNotesMarkdown: |
    - [Find our upstream chart's CHANGELOG here](https://link-goes-here/CHANGELOG.md)
    - [and our upstream application release notes here](https://another-link-here/RELEASE_NOTES.md)
```

## Learn More

- [Application Overview](docs/overview.md)
- [Other Documentation](docs/)

## Pre-Requisites

- Kubernetes Cluster deployed
- Kubernetes config installed in `~/.kube/config`
- Helm installed

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

- Clone down the repository
- cd into directory

```bash
helm install renovate chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| global.commonLabels | object | `{}` | Additional labels to be set on all renovate resources |
| nameOverride | string | `""` | Override the name of the chart |
| fullnameOverride | string | `""` | Override the fully qualified app name |
| cronjob.schedule | string | `"0 1 * * *"` | Schedules the job to run using cron notation |
| cronjob.timeZone | string | `""` | You can specify a time zone for a CronJob by setting timeZone to the name of a valid time zone. (starting with k8s 1.27) <https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/#time-zones> |
| cronjob.suspend | bool | `false` | If it is set to true, all subsequent executions are suspended. This setting does not apply to already started executions. |
| cronjob.annotations | object | `{}` | Annotations to set on the cronjob |
| cronjob.labels | object | `{}` | Labels to set on the cronjob |
| cronjob.concurrencyPolicy | string | `""` | "Allow" to allow concurrent runs, "Forbid" to skip new runs if a previous run is still running or "Replace" to replace the previous run |
| cronjob.completions | string | `""` | "Number of successful completions is reached to mark the job as complete" |
| cronjob.completionMode | string | `""` | "Where the jobs should be NonIndexed or Indexed" |
| cronjob.failedJobsHistoryLimit | string | `""` | Amount of failed jobs to keep in history |
| cronjob.successfulJobsHistoryLimit | string | `""` | Amount of completed jobs to keep in history |
| cronjob.jobRestartPolicy | string | `"Never"` | Set to Never to restart the job when the pod fails or to OnFailure to restart when a container fails |
| cronjob.ttlSecondsAfterFinished | string | `""` | Time to keep the job after it finished before automatically deleting it |
| cronjob.activeDeadlineSeconds | string | `""` | Deadline for the job to finish |
| cronjob.jobBackoffLimit | string | `""` | Number of times to retry running the pod before considering the job as being failed |
| cronjob.startingDeadlineSeconds | string | `""` | Deadline to start the job, skips execution if job misses it's configured deadline |
| cronjob.initContainers | list | `[]` | Additional initContainers that can be executed before renovate |
| cronjob.parallelism | string | `""` | Number of pods to run in parallel |
| cronjob.commandOverride | list | `[]` | Custom command to run in the container |
| cronjob.argsOverride | list | `[]` | Custom arguments to run in the container |
| cronjob.preCommand | string | `""` | Prepend shell commands before renovate runs |
| cronjob.postCommand | string | `""` | Append shell commands after renovate runs |
| pod.annotations | object | `{}` | Annotations to set on the pod |
| pod.labels | object | `{}` | Labels to set on the pod |
| image.registry | string | `"registry1.dso.mil"` | Repository to pull renovate image from |
| image.repository | string | `"ironbank/container-hardening-tools/renovate/renovate"` |  |
| image.tag | string | `"39.83.3"` | Renovate image tag to pull |
| image.pullPolicy | string | `"IfNotPresent"` | "IfNotPresent" to pull the image if no image with the specified tag exists on the node, "Always" to always pull the image or "Never" to try and use pre-pulled images |
| image.useFull | bool | `false` | Set `true` to use the full image. See https://docs.renovatebot.com/getting-started/running/#the-full-image |
| imagePullSecrets | list | `[{"name":"private-registry"}]` | Secret to use to pull the image from the repository |
| renovate.existingConfigFile | string | `""` | Custom exiting global renovate config |
| renovate.config | string | `"{}"` | Inline global renovate config.json |
| renovate.configEnableHelmTpl | bool | `false` | Use the Helm tpl function on your configuration. See README for how to use this value |
| renovate.configIsSecret | bool | `true` | Use this to create the renovate-config as a secret instead of a configmap |
| renovate.securityContext | object | `{"runAsGroup":1001,"runAsNonRoot":true,"runAsUser":1001}` | Renovate Container-level security-context |
| renovate.persistence | object | `{"cache":{"enabled":false,"storageClass":"","storageSize":"512Mi","volumeName":""}}` | Options related to persistence |
| renovate.persistence.cache.enabled | bool | `false` | Allow the cache to persist between runs |
| renovate.persistence.cache.storageClass | string | `""` | Storage class of the cache PVC |
| renovate.persistence.cache.storageSize | string | `"512Mi"` | Storage size of the cache PVC |
| renovate.persistence.cache.volumeName | string | `""` | Existing volume, enables binding the pvc to an existing volume |
| ssh_config.enabled | bool | `false` | Whether to enable the use and creation of a secret containing .ssh files |
| ssh_config.id_rsa | string | `""` | Contents of the id_rsa file |
| ssh_config.id_rsa_pub | string | `""` | Contents of the id_rsa_pub file |
| ssh_config.config | string | `""` | Contents of the config file |
| ssh_config.existingSecret | string | `""` | Name of the existing secret containing a valid .ssh configuration |
| secrets | object | `{}` | Environment variables that should be referenced from a k8s secret, cannot be used when existingSecret is set |
| existingSecret | string | `""` | k8s secret to reference environment variables from. Overrides secrets if set |
| extraConfigmaps | list | `[]` | Additional configmaps. A generated configMap name is: "renovate.fullname" + "extra" + name(below) e.g. renovate-netrc-config |
| extraVolumes | list | `[]` | Additional volumes to the pod |
| extraVolumeMounts | list | `[]` | Additional volumeMounts to the container |
| extraContainers | list | `[]` | Additional containers to the pod |
| serviceAccount.create | bool | `false` | Specifies whether a service account should be created |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.name | string | `""` | The name of the service account to use If not set and create is true, a name is generated using the fullname template |
| resources | object | `{}` | Specify resource limits and requests for the renovate container |
| envFrom | list | `[]` | Environment variables to add from existing secrets/configmaps. Uses the keys as variable name |
| env | object | `{}` | Environment variables to set on the renovate container |
| envList | list | `[]` | Additional env. Helpful too if you want to use anything other than a `value` source. |
| redis.enabled | bool | `false` | Enable the Redis subchart? |
| redis.nameOverride | string | `""` | Override the prefix of the redisHost |
| redis.architecture | string | `"standalone"` | Disable replication by default |
| redis.auth.enabled | bool | `false` | Don't require a password by default |
| redis.kubeVersion | string | `""` | Override Kubernetes version for redis chart |
| hostAliases | list | `[]` | Override hostname resolution |
| securityContext | object | `{"fsGroup":1001,"fsGroupChangePolicy":"OnRootMismatch","runAsGroup":1001,"runAsNonRoot":true,"runAsUser":1001}` | Pod-level security-context |
| nodeSelector | object | `{}` | Select the node using labels to specify where the cronjob pod should run on |
| affinity | object | `{}` | Configure the pod(Anti)Affinity and/or node(Anti)Affinity |
| tolerations | list | `[]` | Configure which node taints the pod should tolerate |
| domain | string | `"bigbang.dev"` | Big Bang Values |
| istio.enabled | bool | `false` |  |
| istio.hardened.enabled | bool | `false` |  |
| istio.hardened.customAuthorizationPolicies | list | `[]` |  |
| istio.mtls.mode | string | `"PERMISSIVE"` | STRICT = Allow only mutual TLS traffic, PERMISSIVE = Allow both plain text and mutual TLS traffic PERMISSIVE is required for any action which redeploys pods because STRICT interferes with initContainers Can be changed to STRICT after all initContainers have finished but will interfere with upgrades/pod deployments that have initContainers |
| istio.renovate.enabled | bool | `true` |  |
| istio.renovate.gateways[0] | string | `"istio-system/public"` |  |
| networkPolicies.enabled | bool | `false` |  |
| networkPolicies.ingressLabels.app | string | `"istio-ingressgateway"` |  |
| networkPolicies.ingressLabels.istio | string | `"ingressgateway"` |  |
| networkPolicies.renovateTargetIpRange | string | `""` | IP range of target deployment |
| networkPolicies.additionalPolicies | list | `[]` |  |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.

---

_This file is programatically generated using `helm-docs` and some BigBang-specific templates. The `gluon` repository has [instructions for regenerating package READMEs](https://repo1.dso.mil/big-bang/product/packages/gluon/-/blob/master/docs/bb-package-readme.md)._

