# 🔸 Exercise 1: Warm Migration Test

## Objective
Perform a warm migration of a virtual machine from a vSphere environment to OpenShift Virtualization using MTV, ensuring that the VM continues running during most of the data transfer.

## Steps

### Step 1: Modify or Create a Warm Migration Plan

```yaml
apiVersion: forklift.konveyor.io/v1beta1
kind: Plan
metadata:
  name: warm-plan
  namespace: openshift-mtv
spec:
  provider:
    source:
      name: vsphere-provider
    destination:
      name: openshift
  map:
    network:
      name: my-network-map
    storage:
      name: my-storage-map
  vms:
    - id: vm-105
  warm: true
```

```bash
oc apply -f warm-plan.yaml
```

### Step 2: Start the Migration

```bash
oc annotate plan warm-plan forklift.konveyor.io/start=true --overwrite
```

### Step 3: Monitor Pre-Cutover Synchronization

Check progress:

```bash
oc get planmigration -n openshift-mtv
```

Wait for replication to complete before proceeding to cutover.

### Step 4: Cutover (Power Down Source)

Finalize migration:

```bash
oc annotate planmigration <migration-name> forklift.konveyor.io/cutover=true
```

### Step 5: Validate Migrated VM

Ensure VM boots and functions properly in OpenShift Virtualization.

---