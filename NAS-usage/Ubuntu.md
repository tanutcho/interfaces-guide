# Mount NAS via Ubuntu

![Ubuntu](https://seeklogo.com/images/U/ubuntu-logo-8FDEC6A07B-seeklogo.com.png)

### Mounting `<SharedFolder>` from NAS to Ubuntu server

```markup
NAS-I: n1-int.myds.me

volume1
├── /Nannapas                        # Private access
volume2
├── /home                            # Full access, 1 TB for each user
└── /Co-Working_Space
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
```

<pre><code>Client: 10.204.100.xxx
<strong>/mnt
</strong>└── &#x3C;MountPoint></code></pre>

### Using SSHFS

* install sshfs

```
sudo apt-get install sshfs
```

* Create the mountpoint

```
mkdir /mnt/<MountPoint>
```

* Invoke SSHFS with your SSH credentials and the remote location to mount

```
sshfs <YourUserName>@n1-int.myds.me:/<SharedFolder> /mnt/<MountPoint>
```

* Unmount the remote FS

```
fusermount -u /mnt/<MountPoint>
```

### Using CIFS

* To mount a Cifs file system, install the following utility

```
sudo apt install cifs-utils
```

* Mount command

```
sudo mount -t cifs -o username=<USERNAME>,password<PASSWORD> \\
//n1-int.myds.me/<SharedFolder> /mnt/<MountPoint>
```

* Umount the remote FS

```
sudo umount <MountPoint>
```
