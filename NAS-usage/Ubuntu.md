# Mount NAS via Ubuntu

![Ubuntu](https://seeklogo.com/images/U/ubuntu-logo-8FDEC6A07B-seeklogo.com.png)

### Mounting `<SharedFolder>` from NAS to Ubuntu server

```
NAS: n1-int.myds.me

volume1
├── brain
│   └── tantan
│   └── file1
├── Tanut_shared
│   └── file1
│   └── file2
└── <SharedFolder>
    └── <subfolder-2>
    └── file1.xyz
```

```
Ubuntu server: 10.204.100.xxx

mount
└── <FolderName>
    └── <subfolder-2>
    └── file1.xyz
```

* install sshfs

```
sudo apt-get install sshfs
```

* mounting

```
mkdir mount/<FolderName>
```

```
sshfs -o default_permissions <YourUserName>@n1-int.myds.me:/<SharedFolder> ~/<FolderName>
```

* to save --> Enter
