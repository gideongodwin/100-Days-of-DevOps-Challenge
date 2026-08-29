## Day 38 - Pull Docker Image

## Task Details:

Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features.
As per details shared with DevOps team, we need to accomplish the following task:

- Pull `busybox:musl` image on `App Server 3` in Stratos DC

- Re-tag (create new tag) this image as `busybox:blog`

## Steps:

1. Connect to App Server 3
    ```
    ssh banner@stapp03
    ```

2. Pull the Docker image `busybox:musl` from the Docker registry.
    ```
    docker pull busybox:musl
    ```

3. Create the new tag
    ```
    docker tag busybox:musl busybox:blog
    ```

4. Verify the images
    ```
    docker images
    ```
