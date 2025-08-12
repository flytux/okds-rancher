helm upgrade -i rancher rancher-latest/rancher \
--set hostname=rancher.local --set bootstrapPassword=admin \
--set replicas=1 --set global.cattle.psp.enabled=false \
--create-namespace -n cattle-system
