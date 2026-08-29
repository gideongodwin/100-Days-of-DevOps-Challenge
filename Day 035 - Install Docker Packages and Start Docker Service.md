## Day 35 - Install Docker Packages and Start Docker Service

## Task Details:

The Nautilus DevOps team aims to containerize various applications following a recent meeting with the application development team. They intend to conduct testing with the following steps:

- Install `docker-ce` and `docker compose` packages on `App Server 3`

- Initiate the `docker` service.

## Steps:

1. Connect to app server 3 and switch to root user
    ```
    ssh banner@stapp03
    ```
    ```
    sudo -i
    ```

2. Install `yum-utils`
    ```
    yum install -y yum-utils
    ```

3. Add the official Docker repository
    ```
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```

4. Install Docker CE and Docker Compose
    ```
    yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

5. Start and Enable the Docker Service
    ```
    systemctl enable --now docker
    ```

6. Verify the service is running
    ```
    systemctl status docker
    ```
