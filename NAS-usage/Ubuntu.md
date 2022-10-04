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
Ubuntu server: 10.204.100.xxx

<MountPoint>
    └── <subfolder-2>
    └── file1.xyz
```

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
