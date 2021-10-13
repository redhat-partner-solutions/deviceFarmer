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

- Check openstf pods and rethinkdb requirements are running:
 
```console
NAME                                        READY   STATUS    RESTARTS   AGE
rethinkdb-ff5dc4cb9-ddltg                   1/1     Running   0          3m19s
farm-openstf-api-7c7b8d5576-g57x4           1/1     Running   0          2m
farm-openstf-triproxy-app-fb7cfdfb5-tggpk   1/1     Running   0          2m
farm-openstf-apk-storage-78b47989b4-ndhb7   1/1     Running   0          2m
farm-openstf-app-7f7b9745cd-pf5fc           1/1     Running   0          2m
farm-openstf-img-storage-6488d7cc47-5rgwd   1/1     Running   0          2m
farm-openstf-auth-5f45f7484f-vvpkb          1/1     Running   0          2m
farm-openstf-processor-69757cd56c-q5hcq     1/1     Running   0          2m
farm-openstf-triproxy-dev-dbcfdbf7f-nqtgj   1/1     Running   0          2m
farm-openstf-reaper-68977d899b-sfw4g        1/1     Running   0          2m
farm-openstf-nginx-74f98974b4-bpk5r         1/1     Running   0          119s
farm-openstf-websocket-58fb67d58f-f455n     1/1     Running   0          119s
farm-openstf-storage-756f5f56c6-bkvrq       1/1     Running   0          119s
farm-openstf-provider-real-n2mtm            2/2     Running   0          2m
```

- Plug phone via USB to the k8s node mounting the USB. Start piloting your remote phone fleet:

![STFscreen](./images/farm.png?raw=true)


- Destroy openSTF:

```
destroy_farmer
```

## Packaging the Chart

For distribution purposes at scale it could be useful to package the helm chart into a single archive file. The helm chart can be packaged by runnning:

```
helm package openstf
```

In this case `openstf` is the path to the location where the chart source is located. The above command will place the archive `openstf-release.tgz` in the directoy you were when you ran the command.