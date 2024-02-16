# OpenStack CLI Cheat Sheet

## Table of Contents
1. [Common Commands](#common-commands)
   - [General](#general)
   - [Authentication](#authentication)
   - [Identity (Keystone)](#identity-keystone)
   - [Images (Glance)](#images-glance)
   - [Compute (Nova)](#compute-nova)
   - [Networking (Neutron)](#networking-neutron)
   - [Block Storage (Cinder)](#block-storage-cinder)
   - [Object Storage (Swift)](#object-storage-swift)
2. [Troubleshooting Commands](#troubleshooting-commands)
   - [General Troubleshooting](#general-troubleshooting)
   - [Nova (Compute Service)](#nova-compute-service)
   - [Neutron (Networking Service)](#neutron-networking-service)
   - [Cinder (Block Storage Service)](#cinder-block-storage-service)
   - [Keystone (Identity Service)](#keystone-identity-service)
   - [Glance (Image Service)](#glance-image-service)
   - [Heat (Orchestration Service)](#heat-orchestration-service)
   - [Logs](#logs)
   - [Networking Diagnostics](#networking-diagnostics)
   - [Resource Clean-Up](#resource-clean-up)
   - [Additional Tips](#additional-tips)
3. [Formatting Tips](#formatting-tips)
   - [General Formatting Options](#general-formatting-options)
   - [Sorting](#sorting)
   - [Filtering](#filtering)
   - [Advanced Formatting](#advanced-formatting)
   - [Tips for Efficiency](#tips-for-efficiency)

---

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
- **Additional volumes are attached post-creation**

1. **Create the Instance with the Boot Volume**:
   - The boot volume contains the operating system and is specified in the `server create` command.
   ```bash
   openstack server create --image IMAGE --flavor FLAVOR --volume BOOT_VOLUME_NAME INSTANCE_NAME
   ```

2. **Attach Additional Volumes After the Instance is Created**:
   - Once the instance is up and running, you can attach additional volumes using the `openstack server add volume` command.
   ```bash
   openstack server add volume INSTANCE_NAME ADDITIONAL_VOLUME_NAME_1
   openstack server add volume INSTANCE_NAME ADDITIONAL_VOLUME_NAME_2
   # Repeat for as many additional volumes as you have
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
  
---

## Formatting Tips

### General Formatting Options
- **Fit-Width**: To ensure output fits the terminal width without wrapping.
  ```bash
  openstack <command> --fit-width
  ```
- **Select Columns**: Display only specified columns in the output.
  ```bash
  openstack <command> -c COLUMN1 -c COLUMN2
  # or
  openstack <command> --column COLUMN1 --column COLUMN2
  ```
- **Output Format**: Display output in different formats like JSON, YAML, or table (default).
  ```bash
  openstack <command> -f json
  openstack <command> -f yaml
  openstack <command> -f table
  ```
- **No Headers**: Hide the table header row in output.
  ```bash
  openstack <command> --no-header
  ```

### Sorting
- **Sort Output**: Sort output by a specific column.
  ```bash
  openstack <command> --sort-column COLUMN_NAME
  ```

### Filtering
- **Filter Output**: Use the `grep` command to filter output.
  ```bash
  openstack <command> | grep 'filter-term'
  ```
- **Combining Commands**: Chain commands with Unix pipes for complex filtering.
  ```bash
  openstack <command> | grep 'filter-term' | awk '{print $1}'
  ```

### Advanced Formatting
- **Custom Scripts**: For complex formatting, consider using custom scripts that parse JSON or YAML output.

### Tips for Efficiency
- **Aliases**: Create shell aliases for commonly used commands with specific formatting.
- **Scripts**: Write shell scripts for complex or frequently used command sequences.
