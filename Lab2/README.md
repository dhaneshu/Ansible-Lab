# Azure VM Playbook

## Lab 2: Deploy Multiple Azure VMs with Ansible

This lab will guide you through the process of deploying multiple virtual machines (VMs) in Azure using Ansible. The playbook automates the creation of networking components, security groups, and VMs based on predefined configurations.

### **Prerequisites**
Ensure you have the following:
- An Azure subscription
- Ansible installed on your machine
- Python 3 and the required Azure modules:
  ```sh
  python3 -m pip install ansible-core azure-cli
  ansible-galaxy collection install azure.azcollection --force
  python3 -m pip install -r ~/.ansible/collections/ansible_collections/azure/azcollection/requirements.txt
  ```

### **Step 1: Clone the Repository**
```sh
git clone git@github.com:dhaneshu/Ansible-Lab.git
cd Ansible-Lab/Lab2
```

### **Step 2: Log in to Azure and Set Subscription**
```sh
az login
az account set --subscription "<your-subscription-id>"
```

### **Step 3: Update the `vars.yaml` File**
Modify the `vars.yaml` file with your desired VM configuration:

```yaml
resource_group_name: NewRG
location: centralus
virtual_network_name: newVnet
address_prefixes: "10.0.0.0/16"
subnet_name: Subnet1
subnet_address_prefix: "10.0.1.0/24"
public_ip_prefix: pip
security_group_name: nsg-ssh
ssh_source_ip: "<your-public-ip>"
network_interface_prefix: myNIC
vm_list:
  - name: vm1
    vm_size: Standard_B2ms
  - name: vm2
    vm_size: Standard_B2ms
  - name: vm3
    vm_size: Standard_B2ms
admin_username: azureuser
ssh_key_data: '<your-ssh-public-key>'
managed_disk_type: Standard_LRS
image_offer: 0001-com-ubuntu-server-jammy
image_publisher: Canonical
image_sku: 22_04-lts
image_version: latest
```

### **Step 4: Run the Ansible Playbook**
Execute the following command to deploy the infrastructure:
```sh
ansible-playbook multi-vm.yaml
```

### **What This Playbook Does**
1. **Creates an Azure Resource Group and Networking Components:**
   - Resource group
   - Virtual network and subnet
   - Network security group (NSG) allowing SSH access
2. **Deploys Multiple Virtual Machines:**
   - Creates public IPs
   - Configures network interfaces
   - Deploys VMs using Ubuntu 22.04 LTS
   - Registers and outputs VM public IP addresses

### **Step 5: Verify Deployment**
To list the deployed VMs in Azure:
```sh
az vm list -d -o table
```

To SSH into a deployed VM:
```sh
ssh azureuser@<vm-public-ip>
```

### **Step 6: Clean Up Resources**
To delete the deployed resources, run:
```sh
ansible-playbook cleanup.yml
```

---

## Conclusion
You have successfully deployed multiple VMs in Azure using Ansible! You can now extend this setup by installing applications or configuring additional networking and security settings.

For troubleshooting, refer to the [Ansible documentation](https://docs.ansible.com/ansible/latest/).

🚀 **Happy Automation!**
