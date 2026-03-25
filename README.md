# Ziyotek DevOps Capstone - Milestone III
*Engineer:* Wais Satari
*Date:* March 2026

## Project Overview
This repository contains the Infrastructure-as-Code (IaC) for a high-availability web application environment. The project demonstrates the automation of a Kubernetes cluster and its integration with a persistent MariaDB database backend.

## 🛠️ Tech Stack
- *Orchestration:* Kubernetes (K8s)
- *Configuration Management:* Ansible
- *Database:* MariaDB (External Node)
- *Infrastructure:* Vagrant / VirtualBox

## How to Deploy
1. Provision VMs using `vagrant up`.
2. **Create the secrets file:** Ansible now expects a file at `vars/secrets.yml`. Create it manually:
   ```bash
   mkdir -p vars
   echo 'db_app_password: "your_password_here"' > vars/secrets.yml
   ```
3. Run the master playbook: `ansible-playbook -i inventory site.yml`.
4. Access the application at http://192.168.56.70:8080/rds.php.
