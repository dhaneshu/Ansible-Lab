
# Lab 1 - Deploy an Azure Virtual Machine Using Ansible

### Clone the Lab Repository

```sh
git clone git@github.com:dhaneshu/Ansible-Lab.git
cd Ansible-Lab
```

### Log in to Azure and Set the Default Subscription

```sh
az login
```

### Generate an SSH Key Pair

```sh
ssh-keygen -m PEM -t rsa -b 4096
```
Press **Enter** for all prompts to accept the default settings.

### Get Your Public IP Address

```sh
curl ifconfig.me
```

### Update `vars.yaml` with Your Inputs

Modify the `vars.yaml` file with the required details:

```yaml
resource_group_name: myResourceGroup
location: centralus
virtual_network_name: myVnet
address_prefixes: "10.0.0.0/16"
subnet_name: mySubnet
subnet_address_prefix: "10.0.1.0/24"
public_ip_name: myPublicIP
security_group_name: myNetworkSecurityGroup
ssh_source_ip: "<your-public-ip>"
network_interface_name: myNIC
vm_name: vm721du
vm_size: Standard_B2ms
admin_username: azureuser
ssh_key_data: '<your-ssh-public-key>'
managed_disk_type: Standard_LRS
image_offer: 0001-com-ubuntu-server-jammy
image_publisher: Canonical
image_sku: 22_04-lts
image_version: latest
```

### Run the Ansible Playbook

```sh
ansible-playbook azurevm.yaml -e "@vars.yaml"
```

This playbook performs the following tasks:
- Creates an Azure Resource Group
- Deploys a Virtual Network and Subnet
- Assigns a Public IP
- Configures a Network Security Group allowing SSH access from your public IP
- Creates a Virtual Network Interface
- Deploys a Virtual Machine with Ubuntu 22.04 LTS


### SSH into the VM
```sh
ssh azureuser@<vm-public-ip>
```

---

## Conclusion

You have now set up Ansible on WSL2 and deployed an Azure VM using an Ansible playbook. You can modify the playbook to deploy additional resources as needed.

For troubleshooting or additional configurations, refer to the [Ansible documentation](https://docs.ansible.com/ansible/latest/).

Happy Automation! 🚀

