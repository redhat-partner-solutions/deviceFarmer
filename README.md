# k8s-deviceFarmer

Manifests to deploy most recent stable release of [openstf](https://github.com/DeviceFarmer/stf) in k8s. The manifests evolve the helm chart from [agoda](https://github.com/agoda-com/android-farm) to the current k8s APIs.

## Quickstart

- Deploy your cluster of choice (in this case a single node k8s cluster):

```
deploy_snc
```

- Deploy openSTF:

```
deploy_farmer
```

- Plug phone via USB to the k8s node mounting the USB. Start piloting your remote phone fleet:

![STFscreen](./images/farm.png?raw=true)

- Destroy openSTF:

```
destroy_farmer
```
