# 🔸 Exercise 2: OVA Import and Migration

## Objective
Simulate a migration using an OVA file as the VM source to import into OpenShift Virtualization.

## Steps

### Step 1: Upload the OVA File

Upload the `.ova` to a PVC or object storage accessible from OpenShift.

```bash
oc create cm my-vm-ova --from-file=vm.ova -n ova-namespace
```

### Step 2: Define OVA Provider

```yaml
apiVersion: forklift.konveyor.io/v1beta1
kind: Provider
metadata:
  name: ova-provider
  namespace: openshift-mtv
spec:
  type: ovirt
  url: "http://example.local/ova-path"
  secret:
    name: ova-access
```

### Step 3: Create Migration Plan

Create a plan pointing to the OVA-based VM.

```yaml
spec:
  provider:
    source:
      name: ova-provider
    destination:
      name: openshift
  ...
```

### Step 4: Start Migration and Validate

Run migration and check that the VM is created and accessible.

---