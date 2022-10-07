# Mount NAS via Docker

![Docker](https://miro.medium.com/max/672/1\*glD7bNJG3SlO0\_xNmSGPcQ.png)

### Mounting `<SharedFolder>` from NAS to docker container

```markup
NAS: n1-int.myds.me
volume1
├── /Nannapas                        # Private access
volume2
├── /home                            # Full access, 1 TB for each user
└── /Co-Working_Space
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
```

```markup
docker container: 10.204.100.192
/mount
└── /<MountPoint>
```

1. Create a container

* add `--device /dev/fuse --cap-add SYS_ADMIN --privileged` when you create `CONTAINER`

Example (Container)

```bash
docker run -ti --name $CONTAINER_NAME \
--gpus $GPU_NUM  --memory=$MEMORY --cpus=$CPU \
-v $YOUR_SRC_PATH:/mount \
-p $PORT:22 \
--device /dev/fuse --cap-add SYS_ADMIN --privileged $IMAGE bash
```

Example (Jupyter Container)

```bash
docker run --rm --gpus=$GPU_NUM \
-ti --net=host -v $YOUR_SRC_PATH:/mount \
--name $CONTAINER_NAME \
--device /dev/fuse --cap-add SYS_ADMIN --privileged
$IMAGE jupyter notebook --ip=0.0.0.0 --allow-root \
--NotebookApp.token='PASSWORD' \
--port $PORT --notebook-dir=/mount
```

1. Access the 'Container' or 'Jupyter'

* attach the 'Container'

```bash
docker attach `CONTAINER_NAME`
```

* or 'Jupyter Container'
  * Go to Jupyter Container URL
  * Create a new terminal: click `New` --> `Terminal`

1. install sshfs

```bash
apt-get update -y
```

```bash
apt-get install sshfs
```

1. mounting

```bash
sshfs -o allow_other,default_permissions <USERNAME>@n1-int.myds.me:/<SharedFolder> \
/mount/<MountPoint>
```

or if you want to use SSH keys for authentication instead of password. [How to use ssh-keygen to generate a new SSH key](https://www.ssh.com/academy/ssh/keygen)

make sure that there is `/.ssh/your_private_key` in `$YOUR_SRC_PATH` in DGX-server

```bash
sshfs -o default_permissions <USERNAME>@n1-int.myds.me:/<SharedFolder> \
/mount/<MountPoint> \
-o IdentityFile=/.ssh/your_private_key
```
