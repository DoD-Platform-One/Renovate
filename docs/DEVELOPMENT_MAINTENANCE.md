# Upgrading the Renovate Package

In most cases renovate will be ran against this repository and flagging new images that are available in Iron Bank for use in upgrading the chart. The image availability is the dependency for upgrading the chart.

When new images are identified as available for this chart - we will want to look to the [upstream chart](https://github.com/renovatebot/helm-charts) and identify the tag release for the chart that contains the image versions we want to upgrade to.

Once the appropriate tag is identified, we will utilize kpt for performing the update

```
kpt pkg update chart/@renovate-${chart.version} --strategy alpha-git-patch
```

# Modifications made to the upstream

### chart/values.yaml
- set registry1 image and imagepullsecret
```yaml
image:
  repository: registry1.dso.mil/ironbank/container-hardening-tools/renovate/renovate
  tag: 34.120.0
  pullPolicy: IfNotPresent

imagePullSecrets:
  - name: private-registry
```
- set to `true` by default to utilize secrets for configs 
```yaml
# -- Use this to create the renovate-config as a secret instead of a configmap
configIsSecret: true
```

- Add in standard Big Bang package values
```yaml
domain: bigbang.dev
istio:
  enabled: false
  mtls:
    # -- STRICT = Allow only mutual TLS traffic,
    # PERMISSIVE = Allow both plain text and mutual TLS traffic
    # PERMISSIVE is required for any action which redeploys pods because STRICT interferes with initContainers
    # Can be changed to STRICT after all initContainers have finished but will interfere with upgrades/pod deployments that have initContainers
    mode: PERMISSIVE
  renovate:
    enabled: true
    gateways:
    - istio-system/public

networkPolicies:
  enabled: false
  ingressLabels: 
    app: istio-ingressgateway
    istio: ingressgateway
  # -- IP range of target deployment
  renovateTargetIpRange: ""

```

### chart/bigbang/*
- Add directory for network policies
- Add peer-authentication resource

# Testing new Renovate Version
Identify a repository with a valid `renovate.json` to execute renovate against.

Deploy Big Bang and orchestrate this package through the `packages` values as such:
```yaml
packages:
  renovate:
    enabled: true
    git:
      repo: https://repo1.dso.mil/big-bang/product/packages/renovate.git
      tag: null
      branch: <branch you are testing>
    values:
      redis:
        enabled: true
      renovate:
        configIsSecret: true
        config: |
          {
            "repositories": ["target/repo"],
            "platform": 'gitlab',
            "endpoint": 'https://repo1.dso.mil/api/v4',
            "token": "<repo1 token>",
            "autodiscover": false,
            "hostRules": [{
              "hostType": "docker",
              "matchHost": "registry1.dso.mil",
              "username": "<registry1 user>",
              "password": "<registry1 secret key>"
            }]
          }
      networkPolicies:
        enabled: "{{ $.Values.networkPolicies.enabled }}"
      istio:
        enabled: "{{ $.Values.istio.enabled }}"
```