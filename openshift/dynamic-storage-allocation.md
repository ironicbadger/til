### OCP Dynamic Storage Allocation

Using annotations it is possible dynamically allocate storage, in this case on Gluster with Heketi.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
 name: something
 annotations:
   volume.beta.kubernetes.io/storage-class: gluster-heketi
spec:
 accessModes:
  - ReadWriteMany
 resources:
   requests:
     storage: 10Gi
```

- Source(s)
  - [ocp-docs](https://docs.openshift.com/container-platform/3.5/install_config/storage_examples/storage_classes_dynamic_provisioning.html)
