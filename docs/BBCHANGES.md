# Changes for Big Bang

## Istio Sidecar

## Redis dependency change

- BB packages should not bring in non-bb charts so bitnami redis was changed to BB redis

### Chart.yaml

- Changed remote redis dependency to local bb package based dependency
