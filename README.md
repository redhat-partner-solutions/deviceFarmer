# k8s-deviceFarmer

Manifests to deploy most recent stable release of [openstf](https://github.com/DeviceFarmer/stf) in k8s. The manifests evolve the helm chart from [agoda](https://github.com/agoda-com/android-farm) to the current k8s APIs.

## Quickstart

Install the chart:

```console
helm install my-farm ./manifests/openstf/
```
This command will create an instance of the chart running in the cluster with the name `my-farm`. To delete the instance from your cluster:

```console
helm delete my-farm 
```

## Step by step deployment

- Step 1) Install [helm](https://helm.sh)

- Step 2) Deploy your cluster of choice (in this case a single node k8s cluster):

```console
deploy_snc
```

The command deploys a K0s cluster on the local machine. Note that this script requires root privileges.

- Step 3 option a) Deploy pre-requirements such as `rethinkdb` and all the deviceFarmer apps in a helm chart:

```console
deploy_farm
```

The above command also uses flannel SDN and metallb to get external access to openstf services. (Root privileges required.)

- Step 3 option b) Assume adb-provider runs using podman in a node outside the k8s cluster. In the node mounting the phone by usb run:

```console
podman play kube usb-phone.yaml
```

- cont Step 3 option b) Deploy pre-requirements and deviceFarmer deployment except the apps needed to mount the phone:

```console
deploy_farm_local_usb
```
	
The above command also uses flannel SDN and metallb to get external access to openstf services. (Root privileges required.)

- Step 4) check that openstf pods and rethinkdb requirements are on a `running` state:
 
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

- Step 5) Plug phone via USB to the k8s node mounting the USB. Start piloting your remote phone fleet:

![STFscreen](./images/farm.png?raw=true)


- Destroy the apps and the cluster:

```console
destroy_farmer
```
 
## Chart description




## Packaging the Chart

For distribution purposes at scale it could be useful to package the helm chart into a single archive file. The helm chart can be packaged by runnning:

```
helm package openstf
```

In this case `openstf` is the path to the location where the chart source is located. The above command will place the archive `openstf-release.tgz` in the directoy you were when you ran the command.

# All-in-one deviceFarmer 

To run device-farmer outside k8s, 
Set the environment variables in the `docker-compose-all.yml`

	* TZ
	* RETHINKDB_PORT_28015_TCP
	* STF_ADMIN_EMAIL
	* STF_ADMIN_NAME

Run `podman-compose` as root to mount the usb:

```
cd manifests/openstf/stf-local/
echo IP=<YOUR_PUBLIC_IP_ADDRESS> >> .env
podman-compose -f docker-compose-all.yml up -d
```
