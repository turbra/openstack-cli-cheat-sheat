# OpenStack CLI Cheat Sheet

## Common Commands

### General
- **List Available Commands**
  ```bash
  openstack --help
  ```

### Authentication
- **Set Environment Variables**
  ```bash
  source openrc.sh
  ```

### Identity (Keystone)
- **List All Users**
  ```bash
  openstack user list
  ```
- **List Identity Service Catalog**
  ```bash
  openstack catalog list
  ```

### Images (Glance)
- **List Images You Can Access**
  ```bash
  openstack image list
  ```
- **Delete Specified Image**
  ```bash
  openstack image delete IMAGE
  ```
- **Describe a Specific Image**
  ```bash
  openstack image show IMAGE
  ```
- **Update Image**
  ```bash
  openstack image set IMAGE
  ```
- **Upload Kernel, RAM, Three-Part, and Raw Images**
  ```bash
  # Various commands for uploading different types of images
  ```

### Compute (Nova)
- **List Instances, Check Status of Instance**
  ```bash
  openstack server list
  ```
- **Create a Flavor Named m1.tiny**
  ```bash
  openstack flavor create --ram 512 --disk 1 --vcpus 1 m1.tiny
  ```
- **List Flavors**
  ```bash
  openstack flavor list
  ```
- **Boot an Instance Using Flavor and Image Names**
  ```bash
  openstack server create --image IMAGE --flavor FLAVOR INSTANCE_NAME
  ```
- **Log in to the Instance, Show Details, View Console Log, Set Metadata, Create Snapshot**
  ```bash
  # Various commands for managing instances
  ```

### Networking (Neutron)
- **Create Network, Create a Subnet**
  ```bash
  openstack network create NETWORK_NAME
  openstack subnet create --subnet-pool SUBNET --network NETWORK SUBNET_NAME
  ```

### Block Storage (Cinder)
- **Create a New Volume, Boot Instance and Attach to Volume**
  ```bash
  openstack volume create --size SIZE_IN_GB NAME
  openstack server create --image IMAGE --flavor FLAVOR --volume VOLUME_NAME INSTANCE_NAME
  ```
- **List Volumes, Attach/Detach a Volume**
  ```bash
  openstack volume list
  openstack server add volume INSTANCE_ID VOLUME_ID
  ```

### Object Storage (Swift)
- **Display Information, List Containers**
  ```bash
  swift stat
  swift list
  ```

---

## Troubleshooting Commands

### General Troubleshooting
- **Show OpenStack Client Version, Service List and Status**
  ```bash
  openstack --version
  openstack service list
  ```

### Nova (Compute Service)
- **Show Instance Details for Troubleshooting**
  ```bash
  openstack server show <server-name>
  ```

### Neutron (Networking Service)
- **Network Agent List and Status, Specific Network Details**
  ```bash
  openstack network agent list
  openstack network show <network-name>
  ```

### Cinder (Block Storage Service)
- **Show Volume Details**
  ```bash
  openstack volume show <volume-name>
  ```

### Keystone (Identity Service)
- **Token Validation**
  ```bash
  openstack token issue
  ```

### Glance (Image Service)
- **Image Details**
  ```bash
  openstack image show <image-name>
  ```

### Heat (Orchestration Service)
- **Stack Events and Details**
  ```bash
  openstack stack event list/show <stack-name>
  ```

### Logs
- **View and Tail Logs**
  ```bash
  tail -f /var/log/<service-name>/<log-file>
  ```

### Networking Diagnostics
- **Ping and Traceroute for Connectivity Issues**

### Resource Clean-Up
- **Force Delete Stuck Resources**
  ```bash
  openstack server delete --force <server-name>
  openstack volume delete --force <volume-name>
  ```

### Additional Tips
- **Structured Output with `-f json` or `-f yaml`**
- **Help Option for Detailed Command Usage**
- **Quota Checks with `openstack quota show`**
- **Regular Service Health Checks**
