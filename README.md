# AlmaLinux-based toolset for APAR

## Objective

Create a common toolset Docker Image to build and run APAR apps/utils

## Build the image

Replace `myuser` and `mypassword` with the desired username/password for the default user:
``` bash
docker build --build-arg USERNAME=myuser --build-arg PASSWORD=mypassword -t alma-linux-qt6 .
``` 

## Run the container

```
docker run -it \
    --name apar_tools \
    -v <LOCAL_PATH>/.ssh:~/.ssh:ro \
    -v <LOCAL_PATH>/projects:~/projects \
    alma-linux-qt6
```

If you are running Docker on Windows \<LOCAL_PATH\> must be absolute path:

```
docker run -it \
    --name apar_tools \
    -v C:/users/user1/.ssh:~/.ssh:ro \
    -v C:/projects:~/projects \
    alma-linux-qt6
```