# Lab 21: Jenkins Role-Based Authorization Strategy

## 📝 Description

This lab demonstrates how to implement **Role-Based Access Control (RBAC)** in Jenkins. The goal is to manage user permissions efficiently by creating specific roles and assigning them to different users.

## 🛠 Prerequisites

* Jenkins Server up and running.
* **Role-based Authorization Strategy** plugin installed.

## 🚀 Implementation Steps

### 1. Plugin Installation

* Installed the **Role-based Authorization Strategy** plugin via `Manage Jenkins` > `Plugins`.
>
> <img width="929" height="724" alt="INSTALL ROLE-BASED AUTH" src="https://github.com/user-attachments/assets/fab12476-0075-4bf5-ad92-503206e66a42" />

### 2. Enabling RBAC

* Navigated to `Manage Jenkins` > `Security`.
* Selected **Role-Based Strategy** under the **Authorization** section.
>
> <img width="940" height="536" alt="SECURITY" src="https://github.com/user-attachments/assets/96339e20-319c-4e91-a193-1be4181be3e6" />

### 3. User Creation

* Created two local users via `Manage Jenkins` > `Users`:
* **user1**: Intended for Administrative access.
* **user2**: Intended for Read-only access.
>
> <img width="940" height="455" alt="users" src="https://github.com/user-attachments/assets/710153c9-ae4e-4ee1-90b5-ce34bba303da" />


### 4. Role Management

* Defined global roles in `Manage Jenkins` > `Manage and Assign Roles` > **Manage Roles**:
* **admin**: Granted all permissions (Full access).
* **readonly**: Granted only `Overall -> Read` permissions.
>
> <img width="949" height="814" alt="readonly" src="https://github.com/user-attachments/assets/dc853e6f-cbf7-4f74-ac8b-07493d69eb24" />


### 5. Role Assignment

* Assigned the defined roles to users in **Assign Roles**:
* Assigned **admin** role to `user1`.
* Assigned **readonly** role to `user2`.
>
> <img width="740" height="735" alt="assign roles" src="https://github.com/user-attachments/assets/70421ee8-b314-459d-ad57-4ddbc34c54b0" />


## ✅ Verification

* **user1**: Logged in and verified full access to system configuration and job management.
>
> <img width="731" height="620" alt="user1 signin" src="https://github.com/user-attachments/assets/e621c7ac-c957-48e3-828c-c66f7e0790db" />
>
> <img width="941" height="886" alt="user1 verify" src="https://github.com/user-attachments/assets/74a9378f-a5c0-470f-b092-0fd5aef37f7c" />

* **user2**: Logged in and verified that the dashboard is visible but "Manage Jenkins" and configuration options are hidden.
>
> <img width="742" height="592" alt="user2 signin" src="https://github.com/user-attachments/assets/112b38b9-2316-4af9-8355-aca645d9f3e3" />
>
> <img width="954" height="647" alt="user2 verify" src="https://github.com/user-attachments/assets/b0b25b56-6aef-4602-91a5-5f850c6eac5b" />
