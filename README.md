# IN WINDOWS (HOST)

## Locate the VM's vdi file
Mine was found in "C:\Users\kvntng\VirtualBox VMs\Ubuntu 18.04.2 LTS\Ubuntu 18.04.2 LTS.vdi"

## Make a copy of the vdi before proceeding

## In Windows Command Prompt
cd “C:\Program Files\Oracle\VirtualBox”

## To resize the virtual disk to 80 GB
VBoxManage modifyhd "C:\Users\kvntng\VirtualBox VMs\Ubuntu 18.04.2 LTS\Ubuntu 18.04.2 LTS.vdi" --resize 81920

## VirtualBox should now detect the change in disk size

# IN LINUX (CLIENT) 

## Use gparted to expand the disk space
gparted

## Find the name of the filesystem
df -h

## Here the name is "/dev/ubuntu-vg/root"
## Resize logical volume
sudo lvresize -r -l 100%VG /dev/mapper/ubuntu--vg-root
## Resize file system
sudo resize2fs /dev/mapper/ubuntu--vg-root
