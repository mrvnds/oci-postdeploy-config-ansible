# oci-postdeploy-config-ansible
Ansible-based automation for OCI post-deployment configuration. This playbook configures the bastion host and connected compute nodes with essential tools and settings required for cloud-native operations.


# 🛠️ OCI Post-Deploy Configuration (Ansible)

This repository provides **Ansible automation** for post-deployment configuration of the bastion host and compute nodes within a Oracle Cloud Infrastructure (OCI) environment.  
It runs after infrastructure provisioning (e.g., via Terraform) and installs key tools, configures system-wide settings (including proxy) and enforces endpoint security.

---

## 🚀 What it does

- Installs common tooling on bastion and nodes:
  - `kubectl` (Kubernetes CLI)
  - `helm` (Kubernetes package manager)
  - `git`
  - `oci-cli` (OCI command line interface)
- Sets up HTTP/HTTPS and `no_proxy` environment variables and system config on all relevant nodes  
- Applies proxy configuration across nodes (bastion + worker/utility nodes)  
- Installs and configures CrowdStrike Falcon Sensor for endpoint protection  
- Enables seamless hand-off from infrastructure provisioning (Terraform) to configuration automation (Ansible)

---

## 🔧 Prerequisites

- A bastion host and compute nodes already provisioned in OCI  
- Ansible control node (or bastion itself) with access to execute playbooks against target hosts  
- SSH connectivity from control node to bastion and then from bastion to compute nodes (or other connectivity as defined)  
- Proxy configuration (if applicable): HTTP/HTTPS proxy host/port, `no_proxy` list  
- CrowdStrike Falcon deployment package/contract/license details (if required)  

---

## ⚙️ Usage

```bash
# Clone the repository
git clone https://github.com/mrvnds/oci-postdeploy-config-ansible.git
cd oci-postdeploy-config-ansible

# Review and update variables in vars/ or group_vars/ (e.g., proxy settings, target hosts, CrowdStrike parameters)

# Run playbook targeting bastion
ansible-playbook -i inventory bastion-setup.yml

# Run playbook for all nodes (via bastion or inventory group)
ansible-playbook -i inventory nodes-setup.yml