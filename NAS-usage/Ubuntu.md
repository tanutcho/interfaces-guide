# Mount NAS via Ubuntu

<img src="https://seeklogo.com/images/U/ubuntu-logo-8FDEC6A07B-seeklogo.com.png" alt="Ubuntu" width="70"/>

### Mounting `<SharedFolder>` from NAS to Ubuntu server

```
NAS: 10.204.100.140

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

- install nfs-common

```console
sudo apt-get install nfs-common
```
- mounting
```console
mkdir mount/<FolderName>
```
```console
sudo mount -t nfs 10.204.100.140:/volume1/<SharedFolder> mount/<FolderName>
```
- Add the following command to the `/etc/fstab` file
```console
sudo nano /etc/fstab
```
```console
  10.204.100.140:/volume1/<SharedFolder>      mount/<FolderName>       nfs       defaults       0       2
```
- to save CTRL+X -->  y --> Enter
