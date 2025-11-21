<!-- Warning: Do not manually edit this file. See notes on gluon + helm-docs at the end of this file for more information. -->
# renovate

![Version: 45.15.1-bb.0](https://img.shields.io/badge/Version-45.15.1--bb.0-informational?style=flat-square) ![AppVersion: 42.15.0](https://img.shields.io/badge/AppVersion-42.15.0-informational?style=flat-square) ![Maintenance Track: bb_integrated](https://img.shields.io/badge/Maintenance_Track-bb_integrated-green?style=flat-square)

Universal dependency update tool that fits into your workflows.

## Upstream References

- <https://github.com/renovatebot/renovate>
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
| domain | string | `"dev.bigbang.mil"` | Big Bang Values |
| istio.enabled | bool | `false` |  |
| istio.hardened.enabled | bool | `false` |  |
| istio.hardened.customAuthorizationPolicies | list | `[]` |  |
| istio.mtls.mode | string | `"STRICT"` | STRICT = Allow only mutual TLS traffic, PERMISSIVE = Allow both plain text and mutual TLS traffic PERMISSIVE is required for any action which redeploys pods because STRICT interferes with initContainers Can be changed to STRICT after all initContainers have finished but will interfere with upgrades/pod deployments that have initContainers |
| istio.renovate.enabled | bool | `true` |  |
| istio.renovate.gateways[0] | string | `"istio-gateway/public-ingressgateway"` |  |
| networkPolicies.enabled | bool | `true` |  |
| networkPolicies.ingressLabels.app | string | `"istio-ingressgateway"` |  |
| networkPolicies.ingressLabels.istio | string | `"ingressgateway"` |  |
| networkPolicies.renovateTargetIpRange | string | `""` | IP range of target deployment |
| networkPolicies.additionalPolicies | list | `[]` |  |
| upstream | object | Upstream chart values | Values to pass to [the upstream renovate chart](https://github.com/renovatebot/helm-charts/blob/renovate-43.13.0/charts/renovate/values.yaml) |
| upstream.image.registry | string | `"registry1.dso.mil"` | Repository to pull renovate image from |
| upstream.image.tag | string | `"42.15.0"` | Renovate image tag to pull |
| upstream.image.pullPolicy | string | `"IfNotPresent"` | "IfNotPresent" to pull the image if no image with the specified tag exists on the node, "Always" to always pull the image or "Never" to try and use pre-pulled images |
| upstream.image.useFull | bool | `false` | Set `true` to use the full image. See https://docs.renovatebot.com/getting-started/running/#the-full-image |
| upstream.imagePullSecrets | list | `[{"name":"private-registry"}]` | Secret to use to pull the image from the repository |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.

---

_This file is programatically generated using `helm-docs` and some BigBang-specific templates. The `gluon` repository has [instructions for regenerating package READMEs](https://repo1.dso.mil/big-bang/product/packages/gluon/-/blob/master/docs/bb-package-readme.md)._

