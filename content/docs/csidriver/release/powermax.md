---
title: PowerMax
description: Release notes for PowerMax CSI driver
---

## Release Notes - CSI PowerMax v2.3.0

### New Features/Changes
- Updated deprecated StorageClass parameter fsType with csi.storage.k8s.io/fstype.
- Added support for Standalone Helm Charts.
- Removed beta volumesnapshotclass sample files.
- Added mapping of PV/PVC to namespace.
- Added support to configure fsGroupPolicy.
- Added support to filter topology keys based on user inputs.
- Added support for SRDF Metro group sharing multiple namespaces.
- Added support for Kubernetes 1.24.
- Added support for OpenShift 4.10.
- Added support to convert replicated volume to non-replicated volume and vice versa for Sync and Async modes.

### Fixed Issues
There are no fixed issues in this release.

### Known Issues

| Issue | Workaround |
|-------|------------|
| Delete Volume fails with the error message: volume is part of masking view | This issue is due to limitations in Unisphere and occurs when Unisphere is overloaded. Currently, there is no workaround for this but it can be avoided by ensuring that Unisphere is not overloaded during such operations. The Unisphere team is assessing a fix for this in a future Unisphere release|
| Getting initiators list fails with context deadline error |  The following error can occur during the driver installation if a large number of initiators are present on the array. There is no workaround for this but it can be avoided by deleting stale initiators on the array|
| Unable to update Host: A problem occurred modifying the host resource | This issue occurs when the nodes do not have unique hostnames or when an IP address/FQDN with same sub-domains are used as hostnames. The workaround is to use unique hostnames or FQDN with unique sub-domains|
| GetSnapVolumeList fails with context deadline error |  The following error can occur if a large number of snapshots are present on the array. There is no workaround for this but it can be avoided by deleting unused snapshots on the array|
| When a node goes down, the block volumes attached to the node cannot be attached to another node | This is a known issue and has been reported at https://github.com/kubernetes-csi/external-attacher/issues/215. Workaround: <br /> 1. Force delete the pod running on the node that went down <br /> 2. Delete the volumeattachment to the node that went down. <br /> Now the volume can be attached to the new node |
| After expanding file system volume , new size is not getting reflected inside the container | This is a known issue and has been reported at https://github.com/dell/csm/issues/378 . Workaround : Remount the volumes <br/> 1. Edit the replica count as 0 in application StatefulSet <br /> 2. Change the replica count as 1 for same StatefulSet. |

### Note:

- Support for Kubernetes alpha features like Volume Health Monitoring and RWOP (ReadWriteOncePod) access mode will not be available in Openshift environment as Openshift doesn't support enabling of alpha features for Production Grade clusters.
