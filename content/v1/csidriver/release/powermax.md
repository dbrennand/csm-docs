---
title: PowerMax
description: Release notes for PowerMax CSI driver
---

## Release Notes - CSI PowerMax v2.2.0

### New Features/Changes
- Added support for new access modes in CSI Spec 1.5.
- Added support for Volume Health Monitoring.
- Added support for Kubernetes 1.23.

### Fixed Issues
There are no fixed issues in this release.

### Known Issues

| Issue | Workaround |
|-------|------------|
| Delete Volume fails with the error message: volume is part of masking view | This issue is due to limitations in Unisphere and occurs when Unisphere is overloaded. Currently, there is no workaround for this but it can be avoided by ensuring that Unisphere is not overloaded during such operations. The Unisphere team is assessing a fix for this in a future Unisphere release|
| Getting initiators list fails with context deadline error |  The following error can occur during the driver installation if a large number of initiators are present on the array. There is no workaround for this but it can be avoided by deleting stale initiators on the array|
| Unable to update Host: A problem occurred modifying the host resource | This issue occurs when the nodes do not have unique hostnames or when an IP address/FQDN with same sub-domains are used as hostnames. The workaround is to use unique hostnames or FQDN with unique sub-domains|
| GetSnapVolumeList fails with context deadline error |  The following error can occur if a large number of snapshots are present on the array. There is no workaround for this but it can be avoided by deleting unused snapshots on the array|

### Note:

- Support for Kubernetes alpha features like Volume Health Monitoring and RWOP (ReadWriteOncePod) access mode introduced in the release will not be available in Openshift environment as Openshift doesn't support enabling of alpha features for Production Grade clusters.
- Expansion of volumes and cloning of volumes are not supported for replicated volumes.
