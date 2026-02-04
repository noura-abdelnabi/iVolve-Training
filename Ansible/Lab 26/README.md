# Lab 26: Ansible Automation Setup & Connectivity (RH294)

## Project Overview

The goal of this lab is to set up an **Ansible Control Node** on Ubuntu and establish a secure, automated connection with a **Red Hat Enterprise Linux (RHEL)** Managed Node.

## Prerequisites

* **Control Node:** Ubuntu OS with Ansible installed.
* **Managed Node:** RHEL 9 VM.
* **Network:** Both VMs are on the same network (Bridge/NAT).

---

## Steps & Implementation

### 1. Inventory Configuration

The first step was defining the Managed Node's IP address in the Ansible inventory file to allow Ansible to track the target machine.

>
> <img width="400" height="676" alt="inventory file" src="https://github.com/user-attachments/assets/7546b687-02b0-4b83-a406-4402e664861a" />

### 2. Establishing SSH Connectivity

To enable passwordless automation, I generated an SSH key pair on the Ubuntu node and transferred the public key to the Red Hat node using the `ssh-copy-id` command.

* **Command used:** `ssh-copy-id root@192.168.86.128`

>
> <img width="973" height="476" alt="copy id   ssh on managed node" src="https://github.com/user-attachments/assets/7d07684a-c513-4975-9498-2fa05732ce58" />

### 3. Verifying Connection (Ad-hoc Command)

I verified the communication between the nodes using the Ansible `ping` module. A "SUCCESS" response confirmed that the Control Node can manage the RHEL server.

* **Command used:** `ansible servers -m ping -i inventory `

>
> <img width="850" height="174" alt="ping" src="https://github.com/user-attachments/assets/825d14cc-ac7c-49d4-9a44-16c9d5852be3" />

### 4. Disk Space Verification (Storage Check)

Before proceeding with the automation tasks, it was mandatory to verify the available disk space on the managed node to ensure sufficient storage for future packages (like Jenkins and Docker).

* **Command used:** `ansible servers -a "df -h" -i inventory `
* **Purpose:** Checking the `/` (root) and `/var` partitions to avoid "No space left on device" errors during Lab 28.

>
> <img width="848" height="224" alt="verify" src="https://github.com/user-attachments/assets/b8bb7a1c-e235-479f-ba38-8c0aa9dfd59f" />

---

## Key Achievements

* Successfully configured Ansible environment.
* Resolved SSH authentication between different Linux distributions.
