# Lab 27: Automated Web Server Deployment (Nginx)

## Project Overview

The objective of this lab was to automate the installation and configuration of the **Nginx Web Server** on a remote RHEL managed node and customize its default landing page using Ansible.

## Implementation Details

### 1. Nginx Package Installation

I created a playbook to ensure the `nginx` package is installed and updated to the latest version on the target machine.

>
> <img width="656" height="456" alt="playbook" src="https://github.com/user-attachments/assets/89e41dc7-625d-498d-8a7b-f03a6e3057f3" />


### 2. Service Management

The playbook was configured to:

* Start the Nginx service.
* Enable the service to start automatically upon system boot.

> 
> <img width="1212" height="440" alt="applying playbook on managed node" src="https://github.com/user-attachments/assets/6da4d228-e962-4d74-a7cf-4e35441de2e1" />


### 3. Website Customization (Index Page)

To verify the deployment, I used the `copy` or `content` module to replace the default Nginx index page with a custom "iVolve" welcome message.

* **Task:** Creating `/usr/share/nginx/html/index.html` with personalized content.

>
> <img width="1215" height="468" alt="verifying web page" src="https://github.com/user-attachments/assets/68247cb9-a6ff-463d-9809-e4d9a24eace0" />


---

## Verification

I verified the success of the lab by:

1. Accessing the Managed Node's IP via a web browser.
2. Running an ad-hoc command to check the service status: `systemctl status nginx`.
