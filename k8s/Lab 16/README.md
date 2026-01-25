# Lab 16: Kubernetes Init Container for Database Setup 🛠️

## Objective

Automate the database schema and user creation process using an **Init Container** to ensure the environment is ready before the main application starts.

## Tasks Performed

* **Init Container Integration:** Modified the `nodejs-app` deployment to include an `initContainer`.
* **MySQL Client Image:** Used the `mysql:5.7` image for the init container to execute database commands.
* **Environment Injection:** Passed database credentials and host information via `ConfigMaps` and `Secrets` to the init container.
* **Automated DB Setup:** The script inside the init container successfully created the `ivolve` database.
* **User & Permissions:** Configured a dedicated user with full privileges on the `ivolve` database.
  
## Screenshot
>
> <img width="874" height="284" alt="init" src="https://github.com/user-attachments/assets/81f279e3-8400-4cba-be71-6cbd79a17c8c" />

---

## Final Verification (Screenshots)

### 1. Database Creation

The `ivolve` database was successfully created by the init container before the application pod started.

> <img width="837" height="455" alt="db ivolve" src="https://github.com/user-attachments/assets/39afb525-9b02-4465-bec6-aefd60d0d853" />


### 2. User Privileges

Verified that the application user exists and has the expected privileges on the database.

> <img width="669" height="196" alt="user" src="https://github.com/user-attachments/assets/5a62ad78-9031-4ea8-9b7f-2040384ae83d" />
