# Lab 29: Securing Sensitive Data with Ansible Vault

## 📌 Project Overview

This lab demonstrates how to use **Ansible Vault** to secure sensitive information while automating the installation and configuration of a MySQL database. The goal is to deploy a secure database environment on a managed node.

---

## 🚀 Lab Implementation Steps

### 1. Encrypting Sensitive Data

We used `ansible-vault` to create an encrypted file named `secret.yaml` to store the database password safely.

>
> <img width="554" height="60" alt="create vault" src="https://github.com/user-attachments/assets/bfe3379b-28ac-4728-a359-08f900412e32" />


### 2. Playbook Development

The playbook was designed to:

* Install MySQL server.
* Install Python dependencies (`PyMySQL`).
* Create the `iVolve` database.
* Create a dedicated user with specific privileges.

>
> <img width="554" height="576" alt="playbook1" src="https://github.com/user-attachments/assets/24ba5aef-97f5-49b0-a6d3-1a003bc2e995" />
>
> <img width="721" height="431" alt="playbook2" src="https://github.com/user-attachments/assets/3a087b45-b7b9-49d0-ac73-44dc474b57f9" />
 

### 3. Execution & Password Prompt

The playbook is executed using the `--ask-vault-pass` flag to decrypt the variables during runtime.

> 
> <img width="1123" height="85" alt="vault pass" src="https://github.com/user-attachments/assets/12c7293c-96fc-4fc4-a3e2-7e88bdd92dc7" />


---

## ✅ Validation & Results

### Database Verification

The final task of the playbook connects to the MySQL instance using the newly created user and lists the available databases to verify success.

### Final Recap

The automation completed successfully with all tasks in "OK" or "Changed" status.

> 
> <img width="981" height="734" alt="apply playbook" src="https://github.com/user-attachments/assets/3c7622b0-626c-4d0e-ae6a-0464423719f0" />


---

## 🛠 Prerequisites

* Ansible installed on Control Node.
* SSH access to the Managed Node.
