# 🔸 Exercise 3: Using Multus Network in VM Migration

## Objective
Migrate a VM to OpenShift Virtualization using a specific Multus secondary network.

## Steps

1. Define a Multus network in your cluster (if not already):

```yaml
apiVersion: "k8s.cni.cncf.io/v1"
kind: NetworkAttachmentDefinition
metadata:
  name: multus-network
  namespace: openshift-mtv
spec:
  config: '{ ... }'
```

2. Add a destination network reference in the `NetworkMap`:

```yaml
destination:
  type: multus
  name: multus-network
```

3. Proceed with creating a migration plan using this map.

4. Validate that the migrated VM is attached to the correct Multus network.

---