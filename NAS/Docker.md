# Mout NAS via Docker

<img src="https://miro.medium.com/max/672/1*glD7bNJG3SlO0_xNmSGPcQ.png" alt="Docker" width="100"/>

- add `--device /dev/fuse --cap-add SYS_ADMIN --privileged` when you create `CONTAINER`

Example

```console
foo@bar:~$ docker run -ti --name $CONTAINER_NAME \
 --gpus $GPU_NUM  --memory=$MEMORY --cpus=$CPU \
 -v $YOUR_SRC_PATH:/mount \
 -p $PORT:22 \
 --device /dev/fuse --cap-add SYS_ADMIN --privileged 
 $IMAGE bash
```

- install sshfs
```console
foo@bar:~$ docker attach `CONTAINER_NAME`
root@container:#$ apt-get update -y
root@container:#$ apt-get install sshfs
```

- mounting
```console
root@container:#$ mkdir /mount/<FolderName>
root@container:#$ sshfs -o allow_other,default_permissions user@<NAS-ip-address>:/<DriveVolumeName> /mount/<FolderName>
```

or if you want to use SSH keys for authentication instead of password, please send public key to me.
[How to use ssh-keygen to generate a new SSH key](https://www.ssh.com/academy/ssh/keygen)
make sure that there is `/.ssh/your_private_key` in `$YOUR_SRC_PATH` in DGX-server
```console
root@container:#$ mkdir /mount/<FolderName>
foo@bar:~$ sshfs -o default_permissions user@<NAS-ip-address>:/<DriveVolumeName> ~/<FolderName> -o IdentityFile=/.ssh/your_private_key
```