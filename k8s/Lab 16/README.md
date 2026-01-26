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
> <img width="676" height="324" alt="init" src="https://github.com/user-attachments/assets/582531c2-3909-46f1-82de-08164cfb8c0b" />

---

## Final Verification (Screenshots)

### 1. Database Creation

The `ivolve` database was successfully created by the init container before the application pod started.

> <img width="948" height="552" alt="db" src="https://github.com/user-attachments/assets/57ea4a3a-1561-4746-ac0b-e31b90ac0459" />


### 2. User Privileges

Verified that the application user exists and has the expected privileges on the database.

> <img width="669" height="196" alt="user" src="https://github.com/user-attachments/assets/5a62ad78-9031-4ea8-9b7f-2040384ae83d" />
