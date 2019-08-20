# Expand usable VirtualBox storage (for ext4 file systems)
This guide details how to expand your VirtualBox VM's storage with a Windows host and a Linux client

## IN WINDOWS (HOST)
### 1. Locate the VM's vdi file
Mine was in "C:\Users\kvntng\VirtualBox VMs\Ubuntu 18.04.2 LTS\Ubuntu 18.04.2 LTS.vdi"

### 2. Make a copy of the vdi before proceeding

### 3. Go to VirtualBox directory in Windows Command Prompt
```
cd “C:\Program Files\Oracle\VirtualBox”
```

### 4. Resize the virtual disk to a desired size
The following command will resize to 80 GB
```
VBoxManage modifyhd "C:\Users\kvntng\VirtualBox VMs\Ubuntu 18.04.2 LTS\Ubuntu 18.04.2 LTS.vdi" --resize 81920
```

### 5. Open VirtualBox. VirtualBox should now detect the change in disk size

## IN LINUX (CLIENT) 

### 1. Use gparted to expand the disk space (physical volume)
```
gparted
```
Use the slider to adjust the space expanded

### 2. Find the name of the filesystem
```
df -h
```
Here the name is "/dev/ubuntu-vg/root" mounted on "/"

### Resize logical volume
This will expand the logical volume to 100% of the physical volume
```
sudo lvresize -r -l 100%VG /dev/mapper/ubuntu--vg-root
```
### Resize file system
This will resize the file system to the full size of the logical volume
```
sudo resize2fs /dev/mapper/ubuntu--vg-root
```
