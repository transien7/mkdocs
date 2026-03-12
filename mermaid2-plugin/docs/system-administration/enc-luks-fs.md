# Encrypted LUKS File Systems

## Creating and Mounting an Encrypted File System
```
fallocate -l <size [100M]> <filename [x]>                        # allocate file size
cryptsetup -y -v luksFormat <path_to_file [x]>                   # create LUKS partition
sudo cryptsetup luksOpen <path_to_file [x]> <mount_name [y]>     # open vault with LUKS
lsblk                                                            # view mounted vault
sudo mkfs.ext4 <path_to_mount [/dev/mapper/y]>                   # format partition
mkdir <directory_name [secret]>                                  # folder to mount to
sudo mount <path_to_mount [/dev/mapper/y]> <directory [secret]>  # mount filesystem
df                                                               # view fs properties
sudo chown <user> <directory [secret]>                           # change ownership
```
The file system can now be interacted with through its directory **secret**, e.g.  
`cp my.file secret/my.file`

## Unmounting the Encrypted File System
```
sudo umount <directory [secret]>            # unmount filesystem
sudo cryptsetup luksClose <mount_name [y]>  # close vault with LUKS
```

## Remounting the File System
```
sudo cryptsetup luksOpen <path_to_file [x]> <mount_name [y]>     # open vault with LUKS
sudo mount <path_to_mount [/dev/mapper/y]> <directory [secret]>  # mount filesystem
```