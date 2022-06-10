# Changes for Big Bang

## Istio Sidecar

### templates/cronjob.yaml

- Added an optional command override when istio is enabled to kill the istio sidecar. Without it the sidecar runs forever and the job is left hanging

## DIND Removal

- dind is not currently compatible with bigbang so to prevent confusion of the end user it was removed from the chart

### templates/_helpers.tpl

- Removed references to dind options under the `renovate.imageTag` definition

### templates/cronjob.yaml

- Removed all ifs and containing yaml referring to the dind values

## Redis dependency change

- BB packages should not bring in non-bb charts so bitnami redis was changed to BB redis 

### Chart.yaml

- Changed remote redis dependency to local bb package based dependency