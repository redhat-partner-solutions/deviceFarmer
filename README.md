# build-deviceFarmer

manifests  to deploy deviceFarmer (openstf) in k8s

## Quickstart

- Deploy your cluster of choice (eg., k0s single node)

```
deploy_snc
```

- Deploy requirements for deviceFarmer

```
deploy_farmer
```

- Plug phone via USB to the k8s node mounting the USB

- Start piloting your remote phone

![STFscreen](./images/farm.png?raw=true)
