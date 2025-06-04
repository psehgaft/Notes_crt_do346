# 🧠 MTV Exercises – 50 Unique Multiple Choice Questions with Explanations

**. What CLI command starts a migration plan?**
  - A) oc launch migration
  - B) oc create planmigration
  - C) oc annotate plan <name> forklift.konveyor.io/start=true
  - D) oc apply -f start-plan.yaml

✅ **Correct Answer:** oc annotate plan <name> forklift.konveyor.io/start=true
ℹ️ **Explanation:** Starting a migration requires annotating the plan resource with the specific key `forklift.konveyor.io/start=true`.

**. What command retrieves logs from the MTV controller?**
  - A) oc logs pod/mtv-ui -n openshift-console
  - B) oc logs deployment/forklift-controller -n openshift-mtv
  - C) oc logs pod/mtv-deployer -n default
  - D) oc get events -n openshift-mtv

✅ **Correct Answer:** oc logs deployment/forklift-controller -n openshift-mtv
ℹ️ **Explanation:** Logs for the MTV controller, which orchestrates migrations, are found in the 'forklift-controller' deployment.

**. What file format is used to define a migration plan in CLI?**
  - A) .cfg
  - B) .yaml
  - C) .json
  - D) .toml

✅ **Correct Answer:** .yaml
ℹ️ **Explanation:** Migration plans are defined as Kubernetes resources using YAML format, which is standard for OpenShift objects.

**. Which annotation is used to trigger a warm migration cutover?**
  - A) forklift.konveyor.io/initiate=true
  - B) forklift.konveyor.io/complete=true
  - C) forklift.konveyor.io/activate=true
  - D) forklift.konveyor.io/cutover=true

✅ **Correct Answer:** forklift.konveyor.io/cutover=true
ℹ️ **Explanation:** The 'cutover' annotation signals MTV to stop the source VM and complete the migration.


**. Where should the OVA file be uploaded for MTV processing?**
  - A) To a local vSphere directory
  - B) To OpenShift ConfigMap or PVC
  - C) Directly on the RHV-M host
  - D) Inside the VM image disk

✅ **Correct Answer:** To OpenShift ConfigMap or PVC
ℹ️ **Explanation:** MTV expects OVA files to be accessible within the OpenShift environment, typically via ConfigMaps or Persistent Volume Claims.

**. Which type is used when defining an OVA provider?** 
  - A) vsphere
  - B) ova
  - C) ovirt
  - D) openshift

✅ **Correct Answer:** ovirt
ℹ️ **Explanation:** The 'ovirt' type is used even when working with OVA imports in MTV, due to shared functionality with RHV.


**. In a NetworkMap, what is the correct type to specify a Multus network?**
  - A) type: multus
  - B) type: openshift
  - C) type: static
  - D) type: dhcp

✅ **Correct Answer:** type: multus
ℹ️ **Explanation:** 'type: multus' indicates that the destination network is a secondary Multus network, not the default pod network.

**. What Kubernetes object defines a Multus network?**
  - A) NetworkMap
  - B) NetworkAttachmentDefinition
  - C) MultusPolicy
  - D) PodNetworkConfig

✅ **Correct Answer:** NetworkAttachmentDefinition
ℹ️ **Explanation:** Multus secondary networks are defined using NetworkAttachmentDefinition (NAD) custom resources.

**. Which object type helps identify import errors in MTV?**
  - A) VirtualMachineImports
  - B) PlanMigrations
  - C) StorageMaps
  - D) MTVLogs

✅ **Correct Answer:** VirtualMachineImports
ℹ️ **Explanation:** VirtualMachineImport CRs contain details about the status of VM import operations and any errors encountered.


**. What is a key feature of a warm migration in MTV?**
  - A) VMs remain powered off during the entire process
  - B) VMs are deleted after migration
  - C) Data is replicated while the VM is running
  - D) Only OVAs are supported for warm migration

✅ **Correct Answer:** Data is replicated while the VM is running
ℹ️ **Explanation:** Warm migration allows the virtual machine to remain operational while data is gradually replicated to the target cluster.




