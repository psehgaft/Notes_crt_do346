# 🔸 Exercise 5: Monitoring and Troubleshooting MTV Logs

## Objective
Learn to collect logs and monitor resources involved in a VM migration for debugging purposes.

## Steps

### Step 1: Watch PlanMigration Status

```bash
oc get planmigration -n openshift-mtv
```

### Step 2: Describe Migration Plan

```bash
oc describe planmigration <name> -n openshift-mtv
```

### Step 3: Collect Logs from MTV Controller

```bash
oc logs deployment/forklift-controller -n openshift-mtv
```

### Step 4: Inspect VirtualMachineImport CRs

```bash
oc get virtualmachineimports -A
```

Use this to detect why a VM may have failed migration.

---