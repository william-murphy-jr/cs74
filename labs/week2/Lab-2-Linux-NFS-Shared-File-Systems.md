# Network File System (NFS) Mount Configuration
Add NFS client mounts of /home and /opt/ohpc/pub to base image:
```
echo "10.1.1.1:/home /home nfs nfsvers=3,nodev,nosuid,noatime 0 0" >> $CHROOT/etc/fstab
echo "10.1.1.1:/opt/ohpc/pub /opt/ohpc/pub nfs nfsvers=3,nodev,noatime 0 0" >> $CHROOT/etc/fstab
```

Export /home and OpenHPC public packages from master server:
```
echo "/home *(rw,no_subtree_check,fsid=10,no_root_squash)" >> /etc/exports
echo "/opt/ohpc/pub *(ro,no_subtree_check,fsid=11)" >> /etc/exports
exportfs -a
systemctl restart nfs-server
systemctl enable nfs-server
```