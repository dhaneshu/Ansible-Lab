# Azure Infrastructure Deployment with Ansible

## Overview
This repository contains Ansible playbooks to automate the deployment of Azure infrastructure, virtual machines, and web server configuration using Nginx. It is designed for knowledge sharing on infrastructure automation with Ansible and Azure.

## Components
### 1. **Infrastructure Deployment (Infra.yaml)**
This playbook creates:
- Azure Resource Group
- Virtual Network and Subnets
- Network Security Groups (NSGs) with rules
- Virtual Machines (VMs) with Public IPs
- Network Interfaces for VMs

### 2. **Application Deployment (app.yaml)**
This playbook:
- Installs and configures Nginx on VMs
- Creates a sample web page
- Configures `iptables` to allow HTTP traffic

### 3. **Azure Dynamic Inventory (azure_rm.yaml)**
- Uses Azure's `azure_rm` plugin to dynamically retrieve VM information
- Filters VMs based on tags (`lab`, `webserver`, `azure-ansible-lab`)

### 4. **Variables Configuration (vars.yaml)**
Defines:
- Resource group, location, and VNet details
- Subnets with NSG rules
- VM details (size, SSH access, OS image)
- Application Gateway settings (if needed)

### 5. **Static Inventory (inventory.txt)**
- Manually defines the web server VMs if dynamic inventory is not used.

## Deployment Steps
### **Step 1: Configure Azure Authentication**
Ensure that your Azure CLI is logged in and configured:
```sh
az login
```

### **Step 2: Verify Inventory**
```sh
ansible-inventory -i azure_rm.yaml --list
```

### **Step 3: Deploy Infrastructure**
```sh
ansible-playbook -i azure_rm.yaml Infra.yaml
```

### **Step 4: Deploy Nginx on VMs**
```sh
ansible-playbook -i azure_rm.yaml app.yaml
```

### **Step 5: Verify Deployment**
Check the public IPs assigned to the VMs:
```sh
cat inventory.txt
```
Access the web server via:
```sh
curl http://<public-ip>
```

## Future Enhancements
- Add SSL/TLS support with Let's Encrypt
- Implement Azure Application Gateway for load balancing
- Automate NSG rule updates dynamically

---
This project demonstrates the power of **Ansible for Infrastructure as Code (IaC)** in **Azure cloud environments**. 🚀

