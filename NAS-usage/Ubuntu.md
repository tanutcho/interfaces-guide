# Mount NAS via Ubuntu

<img src="https://seeklogo.com/images/U/ubuntu-logo-8FDEC6A07B-seeklogo.com.png" alt="Ubuntu" width="70"/>

- install nfs-common

```console
sudo apt-get install nfs-common
```
- mounting
```console
mkdir <path-to>/<FolderName>
```
```console
sudo mount -t nfs 10.204.100.140:/volume1/<DriveVolumeName> <path-to>/<FolderName>
```
- Add the following command to the `/etc/fstab` file
```console
sudo nano /etc/fstab
```
```console
  10.204.100.140:/volume1/<DriveVolumeName>      <path-to>/<FolderName>       nfs       defaults       0       2
```
- to save CTRL+X -->  y --> Enter
