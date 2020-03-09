# Elastic-stack Helm Chart

This chart installs an elasticsearch cluster with kibana and logstash by default.
You can optionally disable logstash and install Fluentd if you prefer. It also optionally installs filebeat, nginx-ldapauth-proxy and elasticsearch-curator.

## Prerequisites Details

* Kubernetes 1.8+ and should't be 1.16.2
* Tested Tiller version 2.15.0 and it won't work in v2.9.1
* PV dynamic provisioning support on the underlying infrastructure

## Chart Details

This chart will do the following:

* Implemented a dynamically scalable elasticsearch cluster using Kubernetes StatefulSets/Deployments
* Multi-role deployment: master, client (coordinating) and data nodes
* Statefulset Supports scaling down without degrading the cluster

## Updating chart dependencies

To update the chart dependencies run:

```bash
$ cd efk-stack
$ helm dep up
$ cd ..
```
This should create a charts/ directory in the project.

## Inspect the Chart config values:

To inspect the chart configs with the release name `telemetry-efk-stack` run:

```bash
$ helm install --dry-run --debug efk-stack -f efk-stack/values-custom.yaml --namespace telemetry --name telemetry-efk-stack
```

## Installing the Chart

To install the chart with the release name `telemetry`:

```bash
$ helm install efk-stack -f efk-stack/values-custom.yaml --namespace telemetry --name telemetry-efk-stack
```

Deployment response will look something like the following

```bash
NOTES:
The elasticsearch cluster and associated extras have been installed.
Kibana can be accessed:

  * Within your cluster, at the following DNS name at port 9200:

    efk-stack-elastic-stack.telemetry.svc.cluster.local

  * From outside the cluster, run these commands in the same shell:

    export NODE_PORT=$(kubectl get --namespace telemetry -o jsonpath="{.spec.ports[0].nodePort}" services efk-stack-elastic-stack)
    export NODE_IP=$(kubectl get nodes --namespace telemetry -o jsonpath="{.items[0].status.addresses[0].address}")
    echo http://$NODE_IP:$NODE_PORT
```

## Port forward Elasticsearch-client and kibana to access the dashboard

For elasticsearch-client:

```bash
$ kubectl port-forward $elasticsearch_client_service 9200 --namespace telemetry
``` 

For Kibana dashboard:
```bash
$ kubectl port-forward $kibana_pod_name 5601 --namespace telemetry
```

## Deleting the Charts

Delete the Helm deployment as normal

```
$ helm delete --purge telemetry-efk-stack
```

Deletion of the StatefulSet doesn't cascade to deleting associated PVCs. To delete them:

```
$ kubectl delete pvc -l release=telemetry,component=data
```

## Configuration

Each requirement is configured with the options provided by that Chart.
Please consult the relevant charts for their configuration options.
