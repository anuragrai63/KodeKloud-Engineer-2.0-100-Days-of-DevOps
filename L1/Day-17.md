# Instructions

The Nautilus application development team has shared that they are planning to deploy a newly developed application on Nautilus infra in Stratos DC. The application uses a PostgreSQL database, so as a prerequisite, a database and user need to be set up for the application.

> **Note:** PostgreSQL database server is already installed on the Nautilus database server.

### Tasks

a. **Create a database user** `kodekloud_sam` and set its password to `Rc5C9EyvbU`.

b. **Create a database** `kodekloud_db10` and grant full permissions to user `kodekloud_sam` on this database.

> **Important:** Please do **not** try to restart the PostgreSQL server service.

---

# Solution

1. **SSH into the database server:**
   ```sh
   ssh peter@stdb01
   ```

2. **Switch to the `postgres` user:**
   ```sh
   sudo -i -u postgres
   ```

3. **Enter the PostgreSQL shell:**
   ```sh
   psql
   ```

4. **Create the user:**
   ```sql
   CREATE USER kodekloud_sam WITH PASSWORD 'Rc5C9EyvbU';
   ```

5. **Create the database:**
   ```sql
   CREATE DATABASE kodekloud_db10;
   ```

6. **Grant all privileges on the database to the user:**
   ```sql
   GRANT ALL PRIVILEGES ON DATABASE kodekloud_db10 TO kodekloud_sam;
   ```

7. **Verify the user and database:**
   - List users:
     ```sql
     \du
     ```
   - List databases:
     ```sql
     \l
     ```

   You should see:
   - `kodekloud_sam` in the user list
   - `kodekloud_db10` in the database list

8. **Exit the PostgreSQL shell and logout:**
   ```sh
   \q
   exit
   ```

9. **Check the result as required.**

---
