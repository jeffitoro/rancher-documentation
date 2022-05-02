---
layout: default
title: Storage
nav_order: 7
---

# Storage
Add storage claims to the workloads.

---

### Allow data size in the configuration file yaml
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/storage/import-volume-storage.png" />](/assets/images/storage/import-volume-storage.png)

### Check your data size allowed
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/storage/persistent-volume-storage.png" />](/assets/images/storage/persistent-volume-storage.png)

### Add data size in the workload services
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/storage/workload-volume-storage.png" />](/assets/images/storage/workload-volume-storage.png)

### Database
```yaml
# Declaration storage claim.
apiVersion: v1
kind: PersistentVolume
metadata:
  name:  borgerhub-data-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 3Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/mnt/data_borgerhub"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name:  borgerhub-data-pvc-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 3Gi
```
