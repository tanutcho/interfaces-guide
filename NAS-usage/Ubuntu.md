# Mount NAS via Ubuntu

![Ubuntu](https://seeklogo.com/images/U/ubuntu-logo-8FDEC6A07B-seeklogo.com.png)

### Mounting `<SharedFolder>` from NAS to Ubuntu server

```
NAS-I: n1-int.myds.me

volume1
└── home
    └── file1
    └── file2

NAS-II: n2-int.myds.me
└── <SharedFolder>
    └── <subfolder-2>
    └── file1.xyz
```

```
Client: 10.204.100.xxx

<MountPoint>
    └── <subfolder-2>
    └── file1.xyz
```

### Using SSHFS

* install sshfs

```
sudo apt-get install sshfs
```

* Create the mountpoint

```
mkdir <MountPoint>
```

* Invoke SSHFS with your SSH credentials and the remote location to mount

```
sshfs <YourUserName>@n2-int.myds.me:/<SharedFolder> <MountPoint>
```

* Unmount the remote FS

```
fusermount -u <MountPoint>
```

### Using CIFS

* To mount a Cifs file system, install the following utility

```
sudo apt install cifs-utils
```

* Mount command

```
sudo mount -t cifs -o username=<USERNAME>,password<PASSWORD> \\
//n1-int.myds.me/<SharedFolder> <MountPoint>
```

* Umount the remote FS

```
sudo umount <MountPoint>
```
