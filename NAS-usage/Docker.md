# Mount NAS via Docker

<img src="https://miro.medium.com/max/672/1*glD7bNJG3SlO0_xNmSGPcQ.png" alt="Docker" width="100"/>

1. Create a container
- add `--device /dev/fuse --cap-add SYS_ADMIN --privileged` when you create `CONTAINER`

Example (Container)

```console
docker run -ti --name $CONTAINER_NAME \
--gpus $GPU_NUM  --memory=$MEMORY --cpus=$CPU \
-v $YOUR_SRC_PATH:/mount \
-p $PORT:22 \
--device /dev/fuse --cap-add SYS_ADMIN --privileged $IMAGE bash
```

Example (Jupyter Container)

```console
docker run --rm --gpus=$GPU_NUM \
-it --net=host -v $YOUR_SRC_PATH:/mount \
--name $CONTAINER_NAME \
--device /dev/fuse --cap-add SYS_ADMIN --privileged \
$IMAGE jupyter notebook --ip=0.0.0.0 --allow-root \
--NotebookApp.token='PASSWORD' \
--port $PORT --notebook-dir=/mount
```

2. Access container
 - attach the Container
```console
docker attach `CONTAINER_NAME`
```

- or Jupyter Container 
  - Go to Jupyter Container URL
  - Create a new terminal: click `New` --> `Terminal`

3. install sshfs
```console
apt-get update -y
```
```console
apt-get install sshfs
```

4. mounting
```console
mkdir /mount/<FolderName>
```
```console
sshfs -o allow_other,default_permissions brain@10.204.100.140:/<SharedFolder> /mount/<FolderName>
```

or if you want to use SSH keys for authentication instead of password.
[How to use ssh-keygen to generate a new SSH key](https://www.ssh.com/academy/ssh/keygen)

make sure that there is `/.ssh/your_private_key` in `$YOUR_SRC_PATH` in DGX-server

```console
sshfs -o default_permissions brain@10.204.100.140:/<SharedFolder> ~/<FolderName> \
-o IdentityFile=/.ssh/your_private_key
```
