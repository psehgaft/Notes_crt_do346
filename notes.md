 - Migration Toolkit for Virtualization (MTV) Operator Install
 - Creating Migration Plans for Virtual Machines (VMs)
    - Creating Providers
    - Creating Storage Maps
    - Creating Network Maps
 - Migrating VMs from Other Hypervisors
    - VMware
    - Red Hat Virtualization (RHV)
    - OpenVirtualAppliances (OVAs)
    - OpenShift Virtualization"


# Step-by-Step Demo: Migrating Virtual Machines with Migration Toolkit for Virtualization (MTV)

This document walks you through the end-to-end process of migrating virtual machines from various sources (VMware, RHV, OVAs, or OpenShift Virtualization) to OpenShift using the **Migration Toolkit for Virtualization (MTV)**. Each step includes both **Web Console (UI)** and **Command-Line Interface (CLI)** instructions.

---

## Prerequisites

- OpenShift 4.12+ cluster with cluster-admin privileges
- OpenShift Virtualization must be installed and configured
- Access to source virtualization environments (vSphere, RHV, etc.)
- Internet access or a configured disconnected environment for MTV operator installation
- `oc` CLI tool installed and authenticated

---

## 1. Install MTV Operator

### Web UI
1. Open the OpenShift Console.
2. Go to `Operators > OperatorHub`.
3. Search for **Migration Toolkit for Virtualization**.
4. Click **Install** using the namespace `openshift-mtv`.
5. Use default settings unless custom requirements apply.

### CLI
```bash
oc new-project openshift-mtv
oc apply -f https://github.com/psehgaft/Notes_crt_do346/blob/main/crds/mtv-operator.yaml
```

---

## 2. Define Providers (VMware, RHV, OVAs, OpenShift Virtualization)

Providers represent the source and destination virtualization environments.

### Web UI
1. Navigate to `MTV > Providers > Create Provider`.
2. Select provider type: `vSphere`, `RHV`, `OVA`, or `OpenShift Virtualization`.
3. Fill in connection details, such as:
   - Provider name
   - Host URL (vCenter, RHV-M, etc.)
   - Credentials or secret reference
   - CA certificates if required

### 💻 CLI
```bash
oc apply -f provider-vsphere.yaml
```

Example `provider-vsphere.yaml`:
```yaml
apiVersion: forklift.konveyor.io/v1beta1
kind: Provider
metadata:
  name: vsphere-provider
  namespace: openshift-mtv
spec:
  type: vsphere
  url: https://vcenter.example.com
  secret:
    name: vsphere-credentials
```

---

## 3. Create Storage Maps

Storage maps map source datastores to OpenShift storage classes.

### Web UI
1. Go to `MTV > Storage Maps > Create`.
2. Select the source and destination providers.
3. Map vSphere/RHV datastores to OpenShift PVC-backed StorageClasses.

### CLI
```bash
oc apply -f storage-map.yaml
```

Example:
```yaml
apiVersion: forklift.konveyor.io/v1beta1
kind: StorageMap
metadata:
  name: my-storage-map
  namespace: openshift-mtv
spec:
  map:
    - source:
        id: datastore-12
      destination:
        storageClass: ocs-storagecluster-ceph-rbd
  source:
    name: vsphere-provider
  destination:
    name: openshift
```

---

## 4. Create Network Maps

Network maps match source VM networks to OpenShift networks (like `pod` or `Multus` networks).

### Web UI
1. Navigate to `MTV > Network Maps > Create`.
2. Select source and destination networks and define their relationship.

### CLI
```bash
oc apply -f network-map.yaml
```

Example:
```yaml
apiVersion: forklift.konveyor.io/v1beta1
kind: NetworkMap
metadata:
  name: my-network-map
  namespace: openshift-mtv
spec:
  map:
    - source:
        id: "VM Network"
      destination:
        type: pod
  source:
    name: vsphere-provider
  destination:
    name: openshift
```

---

## 5. Create a Migration Plan

A migration plan combines providers, storage/network maps, and a list of VMs to be migrated.

### Web UI
1. Go to `MTV > Migration Plans > Create`.
2. Enter plan name and select providers.
3. Choose VMs to migrate.
4. Assign storage and network maps.
5. Select migration type: **Cold** (offline) or **Warm** (replicated while online).

### CLI
```bash
oc apply -f migration-plan.yaml
```

Example:
```yaml
apiVersion: forklift.konveyor.io/v1beta1
kind: Plan
metadata:
  name: test-plan
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
    - id: vm-182
  warm: false
```

---

## 6. Run the Migration

### Web UI
1. Open the migration plan from the list.
2. Click **Start Migration**.
3. Monitor progress through the UI stages:
   - VM preparation
   - Disk transfer
   - Post-migration boot

### CLI
```bash
oc annotate plan test-plan forklift.konveyor.io/start=true --overwrite
```

Check progress:
```bash
oc get planmigration -n openshift-mtv
```

---

## 7. Validate Migrated VMs

### Web UI
- Go to `Virtualization > Virtual Machines`.
- Check VM status, networking, and storage volumes.

### CLI
```bash
oc get vm -n target-namespace
```

---

## Additional Exercises

### 🔸 Exercise 1: Warm Migration Test
1. Modify a migration plan to enable warm migration (`warm: true`).
2. Validate that the incremental disk syncing occurs.
3. Shut down source VM and finalize migration.

### 🔸 Exercise 2: OVA Import
1. Upload OVA file to OpenShift PVC or object storage.
2. Define an OVA provider.
3. Create a migration plan using the OVA image as source.

---

## References

- Red Hat MTV Docs: https://access.redhat.com/documentation/en-us/migration_toolkit_for_virtualization/
- GitHub Forklift Project: https://github.com/kubev2v/forklift
- Network Mapping Docs: https://access.redhat.com/documentation/en-us/migration_toolkit_for_virtualization/latest/html-single/creating_migration_plans/index

---

© 2025 - This demo guide was generated by ChatGPT for OpenShift Virtualization environments.
