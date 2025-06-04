# 🔸 Exercise 4: Full CLI-Only Migration

## Objective
Complete an entire VM migration using only the `oc` CLI.

## Steps

1. Create providers via YAML
2. Define storage and network maps
3. Create the migration plan
4. Start migration and monitor status
5. Validate result

Sample commands:

```bash
oc apply -f provider-vsphere.yaml
oc apply -f storage-map.yaml
oc apply -f network-map.yaml
oc apply -f migration-plan.yaml
oc annotate plan test-plan forklift.konveyor.io/start=true --overwrite
oc get planmigration -n openshift-mtv
```

---