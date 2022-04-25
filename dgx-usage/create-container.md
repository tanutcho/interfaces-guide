# Create Container

## Create container <a href="#create-container" id="create-container"></a>

### Before you begin <a href="#before-you-begin" id="before-you-begin"></a>

### Get Started <a href="#get-started" id="get-started"></a>

#### 1. Login to DGX server <a href="#1-login-to-dgx-server" id="1-login-to-dgx-server"></a>

```
DGX01 : 10.204.100.191: SCADS & VISION 
DGX02 : 10.204.100.192: BRAIN
```

***

#### 2. Create your project directory <a href="#2-create-your-project-directory" id="2-create-your-project-directory"></a>

```
mkdir project1
```

***

#### 3. Create a container <a href="#3-create-a-container" id="3-create-a-container"></a>

1. List resource will be used.
   * Image name: nvcr.io/nvidia/tensorflow:19.11-tf2-py3
   * CPU: 10 cores
   * Memory: 256 GB
   * Number of GPU: 2
   * Container’s name: ist-container
2.  Pull Docker image

    * find Docker images from [NVIDIA NGC](https://scads.ist.vistec.ac.th/cluster/docs/dgx/create-container.html) or list all local images by command `docker images`

    ```
     `docker pull nvcr.io/nvidia/tensorflow:19.11-tf2-py3`
    ```
3.  Create container with previous configuration

    ```
    docker run -ti --name ist-container \
     --gpus 2  --memory=256GB --cpus=10 \
     -v /home/scads/project1:/mount \
     nvcr.io/nvidia/tensorflow:19.11-tf2-py3 bash
    ```

    * Use `--gpus device=DEVICE_ID` to specific GPU device.
    * [Docker run Reference](https://docs.docker.com/engine/reference/run/)

    **Docker flags**

    `--name`: Container’s name\
    `--gpus`: Number of GPUS\
    `--memory`: Memory limit\
    `--cpus`: Number of CPUs\
    `-v`: Mount volume from machine to container, SOURCE:DEST\
    `-p`: Map port from local machine to container, LOCAL\_PORT:CONTAINER\_PORT \\
4.  Access container

    ```
    docker attach ist-container
    ```
5.  Checking GPU is linked to container.

    ```
    nvidia-smi
    ```

    After that you can install whatever you want inside the container.
6. Detach from container `Press Ctrl+P+Q`

***

#### 4. Stop container when finish. <a href="#4-stop-container-when-finish" id="4-stop-container-when-finish"></a>

```
docker stop ist-container
```

## IMPORTANT NOTE <a href="#important-note" id="important-note"></a>

> **Please stop your container after finish to reallocate resource to other users.**

***

### More information <a href="#more-information" id="more-information"></a>

* An exited container(stopped container) will be kept unless you delete it. If you would like to run the container again, just start the container. `docker start $CONTAINER_NAME`
* List all containers `docker ps -a`
