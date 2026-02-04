# Lab 28: Structured Configuration Management with Ansible Roles

## 📌 Project Overview

The objective of this lab was to transition from simple playbooks to a modular **Roles-based architecture**. The project involved deploying a full DevOps toolstack (Docker, Kubectl, and Jenkins) on a **RHEL 9** managed node.

---

## 🏗 Modular Architecture (Roles)

Instead of a single file, the automation was split into three distinct roles for better maintainability:

1. **Docker Role:** Handles repo configuration and engine installation.
2. **Kubectl Role:** Manages binary distribution and installation.
3. **Jenkins Role:** Installs Java dependencies and the Jenkins automation server.
>
> <img width="836" height="158" alt="create roles" src="https://github.com/user-attachments/assets/f9ecb862-db62-49ee-ae6e-1ae49025560d" />


---

## 🚀 Final Execution & Results

After resolving the environment issues, the playbook was executed successfully.

* **Command:** `ansible-playbook playbook.yml -i inventory`
* **Tasks Executed:** 8 tasks (1 Gathering Facts + 7 Role Tasks).
* **Success Rate:** 100% (ok=7, failed=0).

>
> <img width="1047" height="543" alt="playbook applying" src="https://github.com/user-attachments/assets/dcd4dad5-1a61-4b01-8c25-88a9c3d594e1" />

---

## 🔍 Service Verification

Post-deployment, services were verified on the RHEL node:

* **Docker:** Verified using `docker -version`.
* **Kubectl:** Verified uding `kubectl version --client`
* **Jenkins:** Verified using `systemctl status jenkins` and retrieved the initial admin password.
>
> <img width="862" height="578" alt="verifying" src="https://github.com/user-attachments/assets/b3fdd5d6-f238-401d-a482-5bf6945031ff" />
>
>
> <img width="1211" height="726" alt="jenkins" src="https://github.com/user-attachments/assets/d0483358-b469-4b8b-9ecd-a427c2c343ee" />
