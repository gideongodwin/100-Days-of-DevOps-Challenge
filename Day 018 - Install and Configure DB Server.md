## Day 18 - Install and Configure DB Server

## Task Details:

We need to setup a database server on `Nautilus DB Server` in Stratos Datacenter. Please perform the below given steps on DB Server:
  
  - Install/Configure `MariaDB` server

  - Create a database named `kodekloud_db1`
  
  - Create a user called `kodekloud_joy` and set its password to `YchZHRcLkL`
  
  - Grant full permissions to user `kodekloud_joy` on database `kodekloud_db1`

## Steps:

1. SSH into the database server
    ```
    ssh peter@stdb01
    ```

2. Install MariaDB Server
    ```
    sudo yum install -y mariadb-server
    ```

3. Start and Enable MariaDB
    ```
    sudo systemctl enable --now mariadb
    ```

4. Log into MariaDB
    ```
    sudo mysql
    ```

5. 5.Create Database, User, and Grant Privileges:
    ```
    CREATE DATABASE kodekloud_db1;
    CREATE USER 'kodekloud_joy'@'localhost' IDENTIFIED BY 'YchZHRcLkL';
    GRANT ALL PRIVILEGES ON kodekloud_db1.* TO 'kodekloud_joy'@'localhost';
    FLUSH PRIVILEGES;
    ```

6. Exit
    ```
    exit
    ```
