# OpenStack CLI Cheat Sheet

## Common Commands
#### General
- **List Available Commands**
  ```bash
  openstack --help
  ```

#### Authentication
- **Set Environment Variables**
  ```bash
  source openrc.sh
  ```

#### Compute (Nova)
- **List All Instances**
  ```bash
  openstack server list
  ```
- **Create an Instance**
  ```bash
  openstack server create --flavor <flavor> --image <image> --key-name <keypair> --network <network> <server-name>
  ```
- **Delete an Instance**
  ```bash
  openstack server delete <server-name>
  ```
- **List Flavors**
  ```bash
  openstack flavor list
  ```
- **List Images**
  ```bash
  openstack image list
  ```

#### Networking (Neutron)
- **List Networks**
  ```bash
  openstack network list
  ```
- **Create a Network**
  ```bash
  openstack network create <network-name>
  ```
- **Create a Subnet**
  ```bash
  openstack subnet create --network <network-name> --subnet-range <cidr> <subnet-name>
  ```
- **List Ports**
  ```bash
  openstack port list
  ```
- **List Routers**
  ```bash
  openstack router list
  ```

#### Block Storage (Cinder)
- **List Volumes**
  ```bash
  openstack volume list
  ```
- **Create a Volume**
  ```bash
  openstack volume create --size <size-in-gb> <volume-name>
  ```
- **Delete a Volume**
  ```bash
  openstack volume delete <volume-name>
  ```
- **Attach a Volume to an Instance**
  ```bash
  openstack server add volume <server-name> <volume-name>
  ```
- **Detach a Volume from an Instance**
  ```bash
  openstack server remove volume <server-name> <volume-name>
  ```

#### Identity (Keystone)
- **List Projects**
  ```bash
  openstack project list
  ```
- **List Users**
  ```bash
  openstack user list
  ```

#### Image Service (Glance)
- **List Images**
  ```bash
  openstack image list
  ```
- **Create an Image**
  ```bash
  openstack image create --file <file-path> --disk-format qcow2 --container-format bare <image-name>
  ```
- **Delete an Image**
  ```bash
  openstack image delete <image-name>
  ```

#### Orchestration (Heat)
- **List Stacks**
  ```bash
  openstack stack list
  ```
- **Create a Stack**
  ```bash
  openstack stack create -t <template-file> <stack-name>
  ```
- **Delete a Stack**
  ```bash
  openstack stack delete <stack-name>
  ```
----

## Troubleshooting Commands
#### General
- **Show OpenStack Client Version**
  ```bash
  openstack --version
  ```
- **List Services and Their Status**
  ```bash
  openstack service list
  ```

#### Nova (Compute Service)
- **Show Instance Details for Troubleshooting**
  ```bash
  openstack server show <server-name>
  ```
- **List Failed Compute Services**
  ```bash
  openstack compute service list --service nova-compute --long
  ```

#### Neutron (Networking Service)
- **Check Network Agent List and Status**
  ```bash
  openstack network agent list
  ```
- **Show Details of a Specific Network**
  ```bash
  openstack network show <network-name>
  ```
- **Debug a Port (e.g., on a VM)**
  ```bash
  openstack port show <port-id>
  ```

#### Cinder (Block Storage Service)
- **Show Volume Details**
  ```bash
  openstack volume show <volume-name>
  ```
- **List All Failed Cinder Services**
  ```bash
  openstack volume service list
  ```

#### Keystone (Identity Service)
- **Validate Tokens**
  ```bash
  openstack token issue
  ```

#### Glance (Image Service)
- **Show Image Details**
  ```bash
  openstack image show <image-name>
  ```

#### Heat (Orchestration Service)
- **Show Stack Events for Debugging**
  ```bash
  openstack stack event list <stack-name>
  ```

#### Logs
- **View and Tail Logs**: Logs for each service (like Nova, Neutron, Cinder, etc.) are usually located in `/var/log/<service-name>/`. Tail the logs for real-time troubleshooting.
  ```bash
  tail -f /var/log/nova/nova-api.log
  ```

#### Networking
- **Ping Test**: Use ping to check connectivity between instances, or from an instance to an external IP.
- **Traceroute**: Traceroute can help diagnose where in the network path there may be an issue.

#### Resource Clean-Up
- **Force Delete Stuck Resources**: In some cases, resources like instances or volumes may get stuck. Use `--force` to delete them if standard methods fail.
  ```bash
  openstack server delete --force <server-name>
  openstack volume delete --force <volume-name>
  ```

### Additional Tips
- **Use the `-f json` or `-f yaml` Flags** for more structured output, especially useful for scripts.
- **Check for `--help`** on any command for more options and usage details.
- **Always Check Resource Quotas**: Sometimes issues arise simply because quotas are exceeded. Use `openstack quota show` for this.
- **Regular Health Checks**: Periodically check the health of OpenStack services with `openstack service list`.

This cheat sheet covers a range of essential commands across various OpenStack services and is a great starting point for administrators. However, depending on your specific OpenStack setup and the tasks you need to perform, there may be additional commands and options that are relevant.
