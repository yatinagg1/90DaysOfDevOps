# Day 13 – Linux Volume Management (LVM)

## Task
Learn LVM to manage storage flexibly – create, extend, and mount volumes.

**Watch First:** [Linux LVM Tutorial](https://youtu.be/Evnf2AAt7FQ?si=ncnfQYySYtK_2K3c)

---

## Before You Start

Switch to root user:
```bash
sudo -i
```
or
```bash
sudo su
```
No spare disk? Create a virtual one (watch the tutorial):
```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
losetup -fP /tmp/disk1.img
losetup -a   # Note the device name (e.g., /dev/loop0)
```

![alt text](image.png)
1.42GB created to be attached directly without lvm
2+3GB would be combined and attached via lvm

---

## Challenge Tasks

### Task 1: Check Current Storage
Run: `lsblk`, `pvs`, `vgs`, `lvs`, `df -h`

![alt text](image-1.png)

![alt text](image-2.png)


### Task 2: Create Physical Volume
```bash
pvcreate /dev/sdb   # or your loop device
pvs
```

![alt text](image-6.png)


### Task 3: Create Volume Group
```bash
vgcreate devops-vg /dev/sdb
vgs
```
![alt text](image-7.png)

2 Physical Volume(PV) used to create 1 volume group and 0 logical volume(LV)

### Task 4: Create Logical Volume
```bash
lvcreate -L 500M -n app-data devops-vg
lvs
```

![alt text](image-8.png)


### Task 5: Format and Mount
```bash
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```

![alt text](image-9.png)

![alt text](image-10.png)

Below screenshot is to create mount point from single disk (no lvm usage)
1- make file system with mkfs
2- make directory in /mnt
3- mount the disk on that /mnt/ path
4- make /etc/fstab entry so it remain permanent after reboot or system too and does not get unmounted

![alt text](image-3.png)

![alt text](image-5.png)


### Task 6: Extend the Volume
```bash
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```

![alt text](image-11.png)

![alt text](image-12.png)

/mnt/dev-data filesystem is extended by 200MB

![alt text](image-13.png)

extending /mnt/app-data by 1GB

![alt text](image-14.png)

![alt text](image-15.png)

![alt text](image-16.png)
