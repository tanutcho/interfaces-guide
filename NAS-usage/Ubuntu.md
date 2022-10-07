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

<pre class="language-markup"><code class="lang-markup">Client: 10.204.100.xxx
<strong>/mnt
</strong>└── &#x3C;MountPoint></code></pre>

### Using SSHFS

* install sshfs

```bash
sudo apt-get install sshfs
```

* Invoke SSHFS with your SSH credentials and the remote location to mount

```bash
sshfs <USERNAME>@n1-int.myds.me:/<SharedFolder> /mnt/<MountPoint>
```

* Unmount the remote FS

```bash
fusermount -u /mnt/<MountPoint>
```

### Using CIFS

* To mount a Cifs file system, install the following utility

```bash
sudo apt install cifs-utils
```

* Mount command or see [secure cifs guide](https://pastebin.com/5KGSkyQA?fbclid=IwAR2lng9v1AVpfwaWQpwnB4BzjIjgphMxkz5nMKBLo5UB6jJSTsAkyxgFyy0)

```bash
sudo mount -t cifs -o username=<USERNAME>,password<PASSWORD> \
//n1-int.myds.me/<SharedFolder> /mnt/<MountPoint>
```

* Umount the remote FS

```bash
sudo umount /mnt/<MountPoint>
```

