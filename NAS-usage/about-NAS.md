# About NAS

For now, we have 3 NAS server.

### NAS IP address

* [INTERFACES-I All team](http://10.204.100.140:5000/): 10.204.100.140 - n1-int.myds.me
* [INTERFACES-II Public-Private Dataset](http://10.204.100.139:5000/): 10.204.100.139 - n2-int.myds.me
* [INTERFACES-III Sleep team](http://10.204.100.138:5000/): 10.204.100.138 - TBA

```
NAS:

volume1
├── brain
│   └── <subfolder>
│   └── file1
├── tantan
│   └── file1
│   └── file2
├── <SharedFolder>
│   └── <subfolder-2>
│   └── file1.xyz
volume2
├── Tanut_shared
    └── file1
    └── file2
```

### Create a Shared Folder

1. Go to NAS website (above links)
2. [Create a Shared Folder](https://kb.synology.com/th-th/DSM/help/DSM/AdminCenter/file\_share\_create?version=6)
3. [Assign Shared Folder Permissions](https://kb.synology.com/th-th/DSM/help/DSM/AdminCenter/file\_share\_privilege?version=6)
4. [Assign NFS Permissions](https://kb.synology.com/th-th/DSM/help/DSM/AdminCenter/file\_share\_privilege\_nfs?version=6)
