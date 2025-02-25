---
title: "Observability"
linkTitle: "Observability"
weight: 5
Description: >
  Dell EMC Container Storage Modules (CSM) for Observability
---

 [Container Storage Modules](https://github.com/dell/csm) (CSM) for Observability is part of the open-source suite of Kubernetes storage enablers for Dell EMC products.
 
 It is an OpenTelemetry agent that collects array-level metrics for Dell EMC storage so they can be scraped into a Prometheus database. With CSM for Observability, you will gain visibility not only on the capacity of the volumes/file shares you manage with Dell CSM CSI (Container Storage Interface) drivers but also their performance in terms of bandwidth, IOPS, and response time. 
 
 Thanks to pre-packaged Grafana dashboards, you will be able to go through these metrics history and see the topology between a Kubernetes PV (Persistent Volume) and its translation as a LUN or file share in the backend array. This module also allows Kubernetes admins to collect array level metrics to check the overall capacity and performance directly from the Prometheus/Grafana tools rather than interfacing directly with the storage system itself.

Metrics data is collected and pushed to the [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector), so it can be processed, and exported in a format consumable by Prometheus. SSL certificates for TLS between nodes are handled by [cert-manager](https://github.com/jetstack/cert-manager).

CSM for Observability is composed of several services, each living in its own GitHub repository. Contributions can be made to this repository or any of the CSM for Observability repositories listed below. 

{{<table "table table-striped table-bordered table-sm">}}
| Name | Repository | Description |
| ---- | ---------  | ----------- |
| Performance Metrics for PowerFlex | [CSM Metrics for PowerFlex](https://github.com/dell/karavi-metrics-powerflex) | Performance Metrics for PowerFlex captures telemetry data about Kubernetes storage usage and performance obtained through the CSI (Container Storage Interface) Driver for Dell EMC PowerFlex. The metrics service pushes it to the OpenTelemetry Collector, so it can be processed, and exported in a format consumable by Prometheus. Prometheus can then be configured to scrape the OpenTelemetry Collector exporter endpoint to provide metrics so they can be visualized in Grafana. Please visit the repository for more information. |
| Performance Metrics for PowerStore | [CSM Metrics for PowerStore](https://github.com/dell/csm-metrics-powerstore) | Performance Metrics for PowerStore captures telemetry data about Kubernetes storage usage and performance obtained through the CSI (Container Storage Interface) Driver for Dell EMC PowerStore. The metrics service pushes it to the OpenTelemetry Collector, so it can be processed, and exported in a format consumable by Prometheus. Prometheus can then be configured to scrape the OpenTelemetry Collector exporter endpoint to provide metrics so they can be visualized in Grafana. Please visit the repository for more information. |
| Volume Topology | [CSM Topology](https://github.com/dell/karavi-topology) | Topology provides Kubernetes administrators with the topology data related to containerized storage that is provisioned by a CSI (Container Storage Interface) Driver for Dell EMC storage products. Please visit the repository for more information. |
{{</table>}}

## CSM for Observability Capabilities

CSM for Observability provides the following capabilities:

{{<table "table table-striped table-bordered table-sm">}}
| Capability | PowerMax | PowerFlex | Unity | PowerScale | PowerStore |
| - | :-: | :-: | :-: | :-: | :-: |
| Collect and expose Volume Metrics via the OpenTelemetry Collector | no | yes | no | no | yes |
| Collect and expose File System Metrics via the OpenTelemetry Collector | no |  no | no | no | yes |
| Collect and expose export (k8s) node metrics via the OpenTelemetry Collector | no |  yes | no | no | no |
| Collect and expose filesystem capacity metrics via the OpenTelemetry Collector | no | no | no | no | yes |
| Collect and expose block storage capacity metrics via the OpenTelemetry Collector | no | yes | no | no | yes |
| Non-disruptive config changes | no |  yes | no | no | yes |
| Non-disruptive log level changes | no |  yes | no | no | yes |
| Grafana Dashboards for displaying metrics and topology data | no |  yes | no | no | yes |
{{</table>}}

## Supported Operating Systems/Container Orchestrator Platforms

{{<table "table table-striped table-bordered table-sm">}}
| COP/OS | Supported Versions |
|-|-|
| Kubernetes    | 1.20, 1.21, 1.22 |
| Red Hat OpenShift | 4.8, 4.9 |
| Rancher Kubernetes Engine | yes | 
| RHEL          |     7.x, 8.x      |
| CentOS        |     7.8, 7.9     |
{{</table>}}

## Supported Storage Platforms

{{<table "table table-striped table-bordered table-sm">}}
|               | PowerFlex | PowerStore |
|---------------|:-------------------:|:----------------:|
| Storage Array | 3.5.x, 3.6.x | 1.0.x, 2.0.x |
{{</table>}}

## Supported CSI Drivers

CSM for Observability supports the following CSI drivers and versions.
{{<table "table table-striped table-bordered table-sm">}}
| Storage Array | CSI Driver | Supported Versions |
| ------------- | ---------- | ------------------ |
| CSI Driver for Dell EMC PowerFlex | [csi-powerflex](https://github.com/dell/csi-powerflex) | v2.0,v2.1 |
| CSI Driver for Dell EMC PowerStore | [csi-powerstore](https://github.com/dell/csi-powerstore) | v2.0,v2.1 |
{{</table>}}

## Topology Data

CSM for Observability provides Kubernetes administrators with the topology data related to containerized storage. This topology data is visualized using Grafana:
{{<table "table table-striped table-bordered table-sm">}}
| Field                      | Description                                                                                                                                        |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Namespace                  | The namespace associated with the persistent volume claim                                                                                          |
| Persistent Volume          | The name of the persistent volume                                                                                                                  |
| Status                     | The status of the persistent volume. "Released" indicating the persistent volume has a claim. "Bound" indicating the persistent volume has a claim |
| Persistent Volume Claim    | The name of the persistent volume claim associated with the persistent volume                                                                      |
| CSI Driver                 | The name of the CSI driver that was responsible for provisioning the volume on the storage system                                                  |
| Created                    | The date the persistent volume was created                                                                                                         |
| Provisioned Size           | The provisioned size of the persistent volume                                                                                                      |
| Storage Class              | The storage class associated with the persistent volume                                                                                            |
| Storage System Volume Name | The name of the volume on the storage system that is associated with the persistent volume                                                         |
| Storage Pool               | The storage pool name the volume/storage class is associated with                                                                                  |
| Storage System             | The storage system ID or IP address the volume is associated with                                                                                  |
| Protocol                   | The storage system protocol type the volume/storage class is associated with                                                                       |
{{</table>}}
## TLS Encryption

CSM for Observability deployment relies on [cert-manager](https://github.com/jetstack/cert-manager) to manage SSL certificates that are used to encrypt communication between various components. When [deploying CSM for Observability](./deployment), cert-manager is installed and configured automatically.  The cert-manager components listed below will be installed alongside CSM for Observability.

{{<table "table table-striped table-bordered table-sm">}}
| Component |
| --------- |
| cert-manager |
| cert-manager-cainjector |
| cert-manager-webhook |
{{</table>}}

If desired you may provide your own certificate key pair to be used inside the cluster by providing the path to the certificate and key in the Helm chart config. If you do not provide a certificate, one will be generated for you on installation.
> __NOTE__: The certificate provided must be a CA certificate. This is to facilitate automated certificate rotation.

## Viewing Logs

Logs can be viewed by using the `kubectl logs` CLI command to output logs for a specific Pod or Deployment.

For example, the following script will capture logs of all Pods in the CSM namespace and save the output to one file per Pod.

```
#!/bin/bash

namespace=[CSM_NAMESPACE]
for pod in $(kubectl get pods -n $namespace -o name); do
  logFileName=$(echo $pod | tr / -).txt
  kubectl logs -n $namespace $pod --all-containers > $logFileName
done
```
