# Lab 30: Automated Cloud Deployment with Ansible Dynamic Inventory

## 📌 Project Overview

This project demonstrates advanced automation by integrating **Ansible** with **AWS**. Instead of static IP management, we implement **Dynamic Inventory** to automatically discover EC2 instances based on Tags. The lab also covers cross-platform playbook adaptation (migrating from RHEL to Ubuntu).

---

## 🚀 Key Implementation Steps

### 1. AWS Infrastructure & Tagging

* Provisioned an **Ubuntu 24.04 EC2 instance** on AWS.
* Applied a specific tag `service:db` to enable automated discovery.

>
> <img width="1623" height="821" alt="EC2 INSTANCE WITH TAG" src="https://github.com/user-attachments/assets/0a6e9fd7-9b3c-4e43-b831-22a57d42b231" />


### 2. Dynamic Inventory Configuration

* Configured the `amazon.aws.aws_ec2` plugin.
* Verified that Ansible can dynamically fetch the public IP address without manual entry.

>
> <img width="790" height="95" alt="INVENTORY GRAPH" src="https://github.com/user-attachments/assets/48fb5d2f-e798-42c2-9961-46ecb2e20b48" />


---

## ✅ Deployment Results

### Successful Execution

The playbook executed successfully, configuring the database and user while pulling encrypted credentials from **Ansible Vault**.

>
> <img width="1128" height="635" alt="APPLY PLAYBOOK" src="https://github.com/user-attachments/assets/b6fb5ef6-fcd1-4b2a-a71d-5509f32a16a1" />


### Verification

The database `iVolve` and the user `ivolve_user` were successfully created on the remote AWS instance.

>
> <img width="1133" height="345" alt="DATABASES ON EC2" src="https://github.com/user-attachments/assets/9bcfc7be-c504-450e-8624-71fb020f4767" />

---

## 🛠 Tools & Technologies

* **Cloud:** AWS (EC2)
* **Automation:** Ansible (Dynamic Inventory, Vault, Playbooks)
* **OS:** Ubuntu 24.04 (Managed Node)
* **Database:** MySQL Server
