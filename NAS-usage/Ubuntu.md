# Mount NAS via Ubuntu

<img src="https://seeklogo.com/images/U/ubuntu-logo-8FDEC6A07B-seeklogo.com.png" alt="Ubuntu" width="70"/>

- install nfs-common

```console
sudo apt-get install nfs-common
```
- mounting
```console
mkdir <FolderName>
```
```console
sudo mount -t nfs 10.204.100.140:/volume1/<DriveVolumeName> ~/<FolderName>
```
- Add the following command to the `/etc/fstab` file
```console
sudo nano /etc/fstab
```
```console
10.204.100.140:/volume1/<DriveVolumeName>       /home/brain/<FolderName>	nfs	defaults       0       2
```
- to save CTRL+X -->  y --> Enter
# 3. MacOs and Windows
- [MacOS](https://www.synology.com/helpfile/help/DSM/5.2/dsm/enu/Tutorial/store_with_mac.html)
- [Windows](https://www.synology.com/en-global/knowledgebase/DSM/help/DSM/Tutorial/store_with_windows)

# :warning: If you found this error:exclamation: :warning:

```diff
- Connection reset by peer
```
- delete ssh-keygen in `~/.ssh/known_hosts` using this command

```console
foo@bar:~$ ssh-keygen -R 10.204.100.140
```