# Changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)

---
## [37.104.1-bb.1] - 2024-01-17
### Updated
- updated renovate.json to include mission team label

## [37.104.1-bb.0] - 2023-12-19
### Updated
- ghcr.io/renovatebot/renovate - minor - 37.27.0 -> 37.104.1
- gluon - patch - 0.4.4 -> 0.4.5
- redis - minor - 18.0.4-bb.0 -> 18.3.2-bb.1
- registry1.dso.mil/ironbank/bitnami/redis - patch - 7.2.2 -> 7.2.3
- registry1.dso.mil/ironbank/container-hardening-tools/renovate/renovate - minor - 37.27.0 -> 37.91.5

## [37.27.0-bb.1] - 2023-11-27
### Added
- Added istio `allow-nothing` policy
- Added istio `allow-ingress` polic(y|ies)
- Added istio custom policy template
- Added istio `allow-https-port` policy
- Added istio `allow-namespace-com` policy
- Addded istio `allow-dns-port` policy 

## [37.27.0-bb.0] - 2023-11-14
### Changed
- Bumped Redis chart dependency to `18.0.4-bb.0`
- Bumped Gluon chart dependency to `0.4.4`
- Updated redis to `7.2.2`
- Updated redis-exporter to `v1.55.0``
- Updated renovate to `37.27.0`

## [34.120.0-bb.3] - 2023-10-30
### Changed
- Removed an upstream annotation from being managed by our renovate

## [34.120.0-bb.2] - 2023-05-23
### Changed
- Bumped Redis chart dependency to `17.10.2-bb.0`
- Bumped Gluon chart dependency to `0.4.0`
- Updated redis to `7.0.11`

## [34.120.0-bb.1] - 2023-04-07
### Changed
- Updated redis to 7.0.10

## [34.120.0-bb.0] - 2023-03-24
### Changed
- Added standard Network Policies
- Update renovate.json to include `helmv3` manager
- Update redis dependency to reference OCI artifact
- Update to application and chart version to `34.120.0`

## [32.38.0-bb.1] - 2023-03-22
### Added
- Added `renovate.json` configuration to project root for renovate updates

## [32.38.0-bb.0] - 2022-06-09
### Added
- Initial renovate release
