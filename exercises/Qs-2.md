# 🧠 Exam: Networking and Storage in OpenShift Virtualization

### 1. What resource is used to assign a network interface to a VM in OpenShift Virtualization?
- A. NetworkAttachmentDefinition
- B. Service
- C. PersistentVolume
- D. VirtualService
- E. Ingress
- F. StorageClass

**Correct Answer:** NetworkAttachmentDefinition

---
### 2. What is the default network type used by a VM if no specific network is defined?
- A. Pod network (masquerade)
- B. Bridge network
- C. Multus network
- D. External network
- E. Host network
- F. Overlay network

**Correct Answer:** Pod network (masquerade)

---
### 3. Which component defines the interface type (bridge, masquerade, etc.) for a VM's network?
- A. Interface definition in the VM spec
- B. Service definition
- C. CNI plugin
- D. Ingress controller
- E. Pod template
- F. NodeSelector

**Correct Answer:** Interface definition in the VM spec

---
### 4. What is the main difference between `masquerade` and `bridge` in a VM network interface?
- A. `Masquerade` hides VM behind the pod IP; `Bridge` gives direct access to the network.
- B. `Masquerade` provides more bandwidth
- C. `Bridge` is used for internal communication only
- D. `Masquerade` uses VXLAN
- E. `Bridge` is only for Windows VMs
- F. `Masquerade` blocks external traffic

**Correct Answer:** `Masquerade` hides VM behind the pod IP; `Bridge` gives direct access to the network.

---
### 5. Which network type would you use if you want the VM to have outbound Internet access but not be directly accessible from outside the cluster?
- A. Masquerade
- B. Bridge
- C. Multus
- D. Host
- E. External
- F. SR-IOV

**Correct Answer:** Masquerade

---
### 6. How can two VMs directly communicate if they are on the same bridge network?
- A. They use the same Layer 2 network segment
- B. They require a LoadBalancer
- C. They use nodePorts
- D. They connect through a service mesh
- E. They use NAT translation
- F. They require Ingress resources

**Correct Answer:** They use the same Layer 2 network segment

---
### 7. Which resource exposes a VM via an external IP or internal DNS within the cluster?
- A. Service
- B. Ingress
- C. Route
- D. Pod
- E. Volume
- F. Deployment

**Correct Answer:** Service

---
### 8. What is the best option to isolate VMs in separate networks for security reasons?
- A. Use different NetworkAttachmentDefinitions
- B. Create different namespaces
- C. Use firewall rules only
- D. Use headless services
- E. Assign node selectors
- F. Use ConfigMaps

**Correct Answer:** Use different NetworkAttachmentDefinitions

---
### 9. If two VMs need to communicate using private IPs across different namespaces, what networking factor must be considered?
- A. NetworkAttachmentDefinitions must be accessible across namespaces
- B. Use StatefulSets
- C. Define common ConfigMaps
- D. Create shared PVCs
- E. Use Routes
- F. Patch the kubelet

**Correct Answer:** NetworkAttachmentDefinitions must be accessible across namespaces

---
### 10. What is the role of `NetworkAttachmentDefinition` in VM communication?
- A. It defines additional network interfaces for VMs
- B. It defines DNS policies
- C. It handles VM storage
- D. It sets VM CPU limits
- E. It manages user authentication
- F. It controls pod tolerations

**Correct Answer:** It defines additional network interfaces for VMs

---
### 11. What is Multus CNI and what problem does it solve?
- A. It enables attaching multiple network interfaces to a pod or VM
- B. It provides storage scheduling
- C. It manages service discovery
- D. It installs OpenShift operators
- E. It enables pod autoscaling
- F. It installs node drivers

**Correct Answer:** It enables attaching multiple network interfaces to a pod or VM

---
### 12. Which Kubernetes resource associates a secondary network with a VM using Multus?
- A. NetworkAttachmentDefinition
- B. ServiceAccount
- C. PersistentVolumeClaim
- D. ClusterRoleBinding
- E. CustomResourceDefinition
- F. PodDisruptionBudget

**Correct Answer:** NetworkAttachmentDefinition

---
### 13. Can a VM be connected to multiple networks simultaneously? Which mechanism allows this?
- A. Yes, using Multus CNI with multiple interfaces
- B. No, only one network is allowed
- C. Only with host networking
- D. Yes, using PVCs
- E. No, requires external routers
- F. Yes, using InitContainers

**Correct Answer:** Yes, using Multus CNI with multiple interfaces

---
### 14. What is the purpose of defining multiple `interfaces` in a VM spec?
- A. To connect the VM to multiple networks
- B. To assign multiple CPUs
- C. To load multiple images
- D. To mount multiple PVCs
- E. To configure user access
- F. To enable live migration

**Correct Answer:** To connect the VM to multiple networks

---
### 15. What must be installed in the cluster to enable Multus CNI?
- A. Multus CNI plugin
- B. Open vSwitch
- C. Calico operator
- D. Service Mesh
- E. Persistent Volumes
- F. Helm charts

**Correct Answer:** Multus CNI plugin

---
### 16. What does it mean when a VM is 'multihomed'?
- A. It has multiple network interfaces
- B. It has multiple CPUs
- C. It has multiple PVCs
- D. It supports multiple OSes
- E. It runs on multiple nodes
- F. It has multiple IPs on the same interface

**Correct Answer:** It has multiple network interfaces

---
### 17. What kind of scenarios require multihomed VMs?
- A. Network separation, firewalls, routing between networks
- B. High CPU workloads
- C. Storage expansion
- D. User authentication
- E. CRON jobs
- F. Pod scheduling

**Correct Answer:** Network separation, firewalls, routing between networks

---
### 18. What caution must be taken when setting static routes in a VM with multiple interfaces?
- A. Avoid conflicting default gateways
- B. Use ReadWriteMany PVCs
- C. Disable DNS
- D. Mount all volumes as read-only
- E. Limit CPU usage
- F. Pin to single node

**Correct Answer:** Avoid conflicting default gateways

---
### 19. How can you check which network interfaces are active inside a running VM?
- A. `ip a` or `ifconfig` inside the VM
- B. oc get network
- C. oc logs
- D. df -h
- E. kubectl describe pod
- F. ls /dev/net

**Correct Answer:** `ip a` or `ifconfig` inside the VM

---
### 20. Which Linux command shows active routes inside a VM?
- A. `ip route`
- B. lsblk
- C. netstat -d
- D. systemctl status
- E. oc describe vm
- F. ls /etc/routes

**Correct Answer:** `ip route`

---
### 21. What volume type is generally used to define persistent disks for VMs?
- A. PersistentVolumeClaim
- B. ConfigMap
- C. Secret
- D. Service
- E. Pod
- F. ServiceAccount

**Correct Answer:** PersistentVolumeClaim

---
### 22. What OpenShift resource represents a volume that can be reused by multiple VMs but not concurrently?
- A. ReadWriteOnce PVC
- B. ConfigMap
- C. ReadWriteMany PVC
- D. Route
- E. DeploymentConfig
- F. Secret

**Correct Answer:** ReadWriteOnce PVC

---
### 23. What annotation allows a volume to be mounted as `bootable` in a VM?
- A. `bootOrder`
- B. readOnly
- C. ephemeral
- D. liveMigration
- E. terminationGracePeriodSeconds
- F. containerPort

**Correct Answer:** `bootOrder`

---
### 24. Which component imports ISO or QCOW2 images to create VM disks?
- A. Containerized Data Importer (CDI)
- B. Multus
- C. Service Mesh
- D. Prometheus
- E. Cluster Autoscaler
- F. Argo CD

**Correct Answer:** Containerized Data Importer (CDI)

---
### 25. What resource represents the root disk of a VM?
- A. DataVolume
- B. ConfigMap
- C. PersistentVolume
- D. Secret
- E. RoleBinding
- F. Deployment

**Correct Answer:** DataVolume

---
### 26. Which method allows attaching additional persistent storage to an existing VM?
- A. Add a new volume and mount it in the VM spec
- B. Recreate the VM
- C. Edit the node label
- D. Change the kubelet config
- E. Restart the namespace
- F. Patch the CDI deployment

**Correct Answer:** Add a new volume and mount it in the VM spec

---
### 27. What happens if a PVC connected to a running VM is deleted?
- A. The VM may crash or lose data
- B. Nothing happens
- C. It gets re-attached
- D. The VM reschedules
- E. A new PVC is created
- F. The VM enters maintenance mode

**Correct Answer:** The VM may crash or lose data

---
### 28. How can you ensure that a persistent volume is not mounted by another VM?
- A. Use ReadWriteOnce access mode
- B. Use ReadWriteMany
- C. Set accessMode to Shared
- D. Configure Ingress rules
- E. Use a LoadBalancer
- F. Attach a secret

**Correct Answer:** Use ReadWriteOnce access mode

---
### 29. What parameters are needed in a `volume` block to use an existing PVC?
- A. Name and persistentVolumeClaim reference
- B. VolumeMode and StorageClass
- C. Pod IP and DNSPolicy
- D. NodeSelector and HostPath
- E. ContainerPort and EnvVar
- F. Command and Args

**Correct Answer:** Name and persistentVolumeClaim reference

---
### 30. Which tool shows the disk status attached to a VM from the OpenShift Web Console?
- A. VirtualMachine -> Disks tab
- B. Cluster Dashboard
- C. Pod Logs
- D. Service Details
- E. PVC list
- F. Kubelet logs

**Correct Answer:** VirtualMachine -> Disks tab

---
