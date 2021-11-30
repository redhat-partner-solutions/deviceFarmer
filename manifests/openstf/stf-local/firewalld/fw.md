# Enable STF access

```console
firewall-cmd --new-service-from-file=manifests/openstf/stf-local/firewalld/stf.xml --permanent
firewall-cmd --zone=public --add-service=stf
```
