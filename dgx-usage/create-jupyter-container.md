# Create Jupyter Container

### Run Jupyter in compute node <a href="#run-jupyter-in-compute-node" id="run-jupyter-in-compute-node"></a>

This tutorial will you how to create a Docker container and Jupyter inside. By default, running Jupyter in local machine use port 8888 to expose notebook service.

So, you need to blind compute node’s port (server’s port) to your local machine using SSH service.

### Get Started <a href="#get-started" id="get-started"></a>

#### 1. Login to DGX server <a href="#1-login-to-dgx-server" id="1-login-to-dgx-server"></a>

```bash
DGX01 : 10.204.100.191: SCADS & VISION 
DGX02 : 10.204.100.192: BRAIN
```

***

#### 2. Create your project directory <a href="#2-create-your-project-directory" id="2-create-your-project-directory"></a>

```bash
mkdir project1
```

***

#### 3. Create a Jupyter container <a href="#3-create-a-jupyter-container" id="3-create-a-jupyter-container"></a>

1. Define resource & port
   * Image name: tensorflow/tensorflow:latest-gpu-jupyter
   * CPU: 10 cores
   * Memory: 256 GB
   * Number of GPU: 1
   * Container’s name: ist-container
   * Jupyter’s Port: 8890
   * Jupyter’s token: password
2.  Pull image

    ```bash
    docker pull tensorflow/tensorflow:latest-gpu-jupyter 
    ```
3.  Create container with previous configuration

    ```bash
    docker run -ti --name ist-container \
     --gpus 1  --memory=256GB --cpus=10 \
     -v /home/scads/project1:/mount \
     -p 8890:8888 \
     tensorflow/tensorflow:latest-gpu-jupyter \
     jupyter notebook --ip=0.0.0.0 --allow-root --NotebookApp.token="password" --port 8888 --notebook-dir=/mount
    ```

    * Use `--gpus device=DEVICE_ID` to specific GPU device.
    * [Official Docker run reference](https://docs.docker.com/engine/reference/run/)

    **IMPORTANT NOTE**

    > Port conflict happens when using the same port as other users/services. Available port range (6000-9000)

    **Docker flags**

    `--name`: Container’s name\
    `--gpus`: Number of GPUS\
    `--memory`: Memory limit\
    `--cpus`: Number of CPUs\
    `-v`: Mount volume from machine to container, SOURCE:DEST\
    `-p`: Map port from local machine to container, LOCAL\_PORT:CONTAINER\_PORT \\

    **Jupyter flag**

    `--allow-root`: Allow running by root user. By default, process in container run by root user\
    `--NotebookApp.token`: Roken for authentication when access Jupyter on browser\
    `--notebook-dir`: The directory in container for notebooks \\
4. Detach from container `Ctrl+P+Q`
5.  In your local machine, start new terminal and run this command to blind Jupyter port.

    ```bash
    ssh -L 8888:10.204.100.191:8890 scads1@$10.204.100.191
    ```
6. Access Jupyter Notebook from your browser `localhost:8888`

***

#### 4. Stop container <a href="#4-stop-container" id="4-stop-container"></a>

1. In local machine terminal, exit SSH session.
2. In server, stop container `docker stop ist-container`
