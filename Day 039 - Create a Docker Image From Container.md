## Day 39 - Create a Docker Image From Container

## Task Details:

One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:

- Create an image `cluster:datacenter` on `Application Server 2` from a container `ubuntu_latest` that is running on same server.

## Steps:

1. Connect to App Server 2
    ```
    ssh steve@stapp02
    ```

2. Confirm `ubuntu_latest` is running
    ```
    docker ps
    ```

3. Create the new image from the container
    ```
    docker commit ubuntu_latest cluster:datacenter
    ```

4. Verify the image
    ```
    docker images
    ```
