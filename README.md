# Ziyotek DevOps Capstone - Milestone III
**Engineer:** Wais Satari  
**Date:** March 2026

## Project Overview
This repository contains the Infrastructure-as-Code (IaC) for a high-availability web application environment. The project demonstrates the automation of a Kubernetes cluster and its integration with a persistent MariaDB database backend.

## 🛠️ Tech Stack
* **Orchestration:** Kubernetes (K8s)
* **Configuration Management:** Ansible
* **Database:** MariaDB (External Node)
* **Infrastructure:** Vagrant / VirtualBox
* **Language:** PHP / SQL

## Repository Structure
* `/kubernetes-manifests`: Contains the K8s Deployment and Service YAML files.
* `/archive`: Legacy configuration scripts from Sprints 1 and 2.
* `site.yml`: Master Ansible playbook for environment provisioning.
* `inventory`: Static inventory mapping the multi-node infrastructure.

## How to Deploy
1. Provision VMs using `vagrant up`.
2. Run the master playbook: `ansible-playbook -i inventory site.yml`.
3. Access the application at `http://192.168.56.70:8080/rds.php`.
