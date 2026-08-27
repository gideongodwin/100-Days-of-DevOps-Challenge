## Day 27- Git Revert Some Changes

## Task Details:

The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/media` present on `Storage server` in Stratos DC.
However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo `HEAD` to last commit.
Below are more details about the task:

  - In `/usr/src/kodekloudrepos/media` git repository, revert the latest commit `HEAD` to the previous commit (JFYI the previous commit hash should be with initial commit message ).
 
      > Use revert media message (please use all small letters for commit message) for the new revert commit.

## Steps:

1. SSH into the Storage Server and switch to root user
    ```
    ssh natasha@ststor01
    ```
    ```
    sudo -i
    ```

2. Navigate to the repository
    ```
    cd /usr/src/kodekloudrepos/media
    ```

3. Check Git History to confirm `HEAD` is the commit you want to revert.
    ```
    git log --oneline
    ```

4. Revert the latest commit
    ```
    git revert --no-commit HEAD 
    ```

5. Commit with the required message in lowercase
    ```
    git commit -m "revert media"
    ```

6. Verify the final commit at HEAD has the correct message.
    ```
    git log --oneline -2
    ```
