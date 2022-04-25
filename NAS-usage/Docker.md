# Mount NAS via Docker

<img src="https://miro.medium.com/max/672/1*glD7bNJG3SlO0_xNmSGPcQ.png" alt="Docker" width="100"/>

- add `--device /dev/fuse --cap-add SYS_ADMIN --privileged` when you create `CONTAINER`

Example

```console
docker run -ti --name $CONTAINER_NAME \
--gpus $GPU_NUM  --memory=$MEMORY --cpus=$CPU \
-v $YOUR_SRC_PATH:/mount \
-p $PORT:22 \
--device /dev/fuse --cap-add SYS_ADMIN --privileged 
$IMAGE bash
```

- install sshfs
```console
docker attach `CONTAINER_NAME`
```
```console
apt-get update -y
```
```console
apt-get install sshfs
```

- mounting
```console
mkdir /mount/<FolderName>
```
```console
sshfs -o allow_other,default_permissions brain@10.204.100.140:/<DriveVolumeName> /mount/<FolderName>
```

or if you want to use SSH keys for authentication instead of password, please send public key to me.
[How to use ssh-keygen to generate a new SSH key](https://www.ssh.com/academy/ssh/keygen)
make sure that there is `/.ssh/your_private_key` in `$YOUR_SRC_PATH` in DGX-server

```console
sshfs -o default_permissions brain@10.204.100.140:/<DriveVolumeName> ~/<FolderName> \
-o IdentityFile=/.ssh/your_private_key
```