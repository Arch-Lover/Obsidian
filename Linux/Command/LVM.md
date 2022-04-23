![[2021-10-09_12-25 1.png]]

PV —> Physical volume

VG —> Volume group

LV —> Logical volume

```bash
toor@debian:~$ sudo pvs
[sudo] password for toor:
  PV         VG        Fmt  Attr PSize   PFree
  /dev/sda5  debian-vg lvm2 a--  <19.52g    0
```

```bash
toor@debian:~$ sudo pvdisplay
  --- Physical volume ---
  PV Name               /dev/sda5
  VG Name               debian-vg
  PV Size               19.52 GiB / not usable 2.00 MiB
  Allocatable           yes (but full)
  PE Size               4.00 MiB
  Total PE              4997
  Free PE               0
  Allocated PE          4997
  PV UUID               DztWM1-DshL-zWUZ-gmsw-IbcX-Keb1-a0GKzT
```

```bash
root@debian:/home/toor# pvcreate /dev/sdb
  Physical volume "/dev/sdb" successfully created.
root@debian:/home/toor# pvs
  PV         VG        Fmt  Attr PSize   PFree
  /dev/sda5  debian-vg lvm2 a--  <19.52g    0
  /dev/sdb             lvm2 ---    8.00g 8.00g
```

```bash
root@debian:/home/toor# pvremove /dev/sdb
  Labels on physical volume "/dev/sdb" successfully wiped.
```

```bash
root@debian:/home/toor# pvcreate /dev/sdb
  Physical volume "/dev/sdb" successfully created.
root@debian:/home/toor# pvs
  PV         VG        Fmt  Attr PSize   PFree
  /dev/sda5  debian-vg lvm2 a--  <19.52g    0
  /dev/sdb             lvm2 ---    8.00g 8.00g
root@debian:/home/toor# pvcreate /dev/sdc
  Physical volume "/dev/sdc" successfully created.
root@debian:/home/toor# pvs
  PV         VG        Fmt  Attr PSize   PFree
  /dev/sda5  debian-vg lvm2 a--  <19.52g    0
  /dev/sdb             lvm2 ---    8.00g 8.00g
  /dev/sdc             lvm2 ---    8.00g 8.00g
```

```bash
root@debian:/home/toor#  vgs
  VG        #PV #LV #SN Attr   VSize   VFree
  debian-vg   1   5   0 wz--n- <19.52g    0
```

```bash
root@debian:/home/toor# vgdisplay
  --- Volume group ---
  VG Name               debian-vg
  System ID
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  6
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                5
  Open LV               5
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <19.52 GiB
  PE Size               4.00 MiB
  Total PE              4997
  Alloc PE / Size       4997 / <19.52 GiB
  Free  PE / Size       0 / 0
  VG UUID               4Dp7WH-gx0l-UwLy-p6g4-EjdR-KB57-ANHMfw
```

```bash
root@debian:/home/toor# vgcreate vg-01 /dev/sdb /dev/sdc
  Volume group "vg-01" successfully created
root@debian:/home/toor# vgs
  VG        #PV #LV #SN Attr   VSize   VFree
  debian-vg   1   5   0 wz--n- <19.52g     0
  vg-01       2   0   0 wz--n-  15.99g 15.99g
```

```bash
root@debian:/home/toor# pvdisplay
  --- Physical volume ---
  PV Name               /dev/sdb
  **VG Name               vg-01**
  PV Size               8.00 GiB / not usable 4.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              2047
  Free PE               2047
  Allocated PE          0
  PV UUID               TYRx7p-TH9X-A61x-W6t3-jVyi-OeVo-a5p4ei

  --- Physical volume ---
  PV Name               /dev/sdc
  VG Name               vg-01
  PV Size               8.00 GiB / not usable 4.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              2047
  Free PE               2047
  Allocated PE          0
  PV UUID               2Mj0jh-k8zU-X0Vf-NzbI-Wqd3-Hzj9-lIEtL6
```

```bash
root@debian:/home/toor# vgrename vg-01 vg-01-reza
  Volume group "vg-01" successfully renamed to "vg-01-reza"
```

```bash
root@debian:/home/toor# vgre
vgreduce  vgremove  vgrename
root@debian:/home/toor# vgremove vg-01
  Volume group "vg-01" successfully removed

root@debian:/home/toor# pvdisplay

  "/dev/sdb" is a new physical volume of "8.00 GiB"
  --- NEW Physical volume ---
  PV Name               /dev/sdb
  VG Name
  PV Size               8.00 GiB
  Allocatable           NO
  PE Size               0
  Total PE              0
  Free PE               0
  Allocated PE          0
  PV UUID               TYRx7p-TH9X-A61x-W6t3-jVyi-OeVo-a5p4ei

  "/dev/sdc" is a new physical volume of "8.00 GiB"
  --- NEW Physical volume ---
  PV Name               /dev/sdc
  VG Name
  PV Size               8.00 GiB
  Allocatable           NO
  PE Size               0
  Total PE              0
  Free PE               0
  Allocated PE          0
  PV UUID               2Mj0jh-k8zU-X0Vf-NzbI-Wqd3-Hzj9-lIEtL6
```

```bash
root@debian:/home/toor# vgs
  VG        #PV #LV #SN Attr   VSize   VFree
  debian-vg   1   5   0 wz--n- <19.52g     0
  vg-01       2   0   0 wz--n-  15.99g 15.99g
root@debian:/home/toor# vgreduce vg-01 /dev/sdc
  Removed "/dev/sdc" from volume group "vg-01"
```

```bash
root@debian:/home/toor# vgextend vg-01 /dev/sdc
  Volume group "vg-01" successfully extended
```

```bash
root@debian:/home/toor# vgscan
  Found volume group "vg-01" using metadata type lvm2
  Found volume group "debian-vg" using metadata type lvm2
root@debian:/home/toor# pvscan
  PV /dev/sdb    VG vg-01           lvm2 [<8.00 GiB / <8.00 GiB free]
  PV /dev/sdc    VG vg-01           lvm2 [<8.00 GiB / <8.00 GiB free]
  PV /dev/sda5   VG debian-vg       lvm2 [<19.52 GiB / 0    free]
  Total: 3 [35.51 GiB] / in use: 3 [35.51 GiB] / in no VG: 0 [0   ]
```

```bash
root@debian:/home/toor# lvcreate -n lv01 vg-01 -L 5G
  Logical volume "lv01" created.

root@debian:/home/toor# lvs
  LV     VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  home   debian-vg -wi-ao---- <12.53g
  root   debian-vg -wi-ao----   4.03g
  swap_1 debian-vg -wi-ao---- 976.00m
  tmp    debian-vg -wi-ao---- 364.00m
  var    debian-vg -wi-ao----   1.65g
  lv01   vg-01     -wi-a-----   5.00g
```

```bash
root@debian:/home/toor# lvremove vg-01/lv01
Do you really want to remove active logical volume vg-01/lv01? [y/n]: y
  Logical volume "lv01" successfully removed
```

```bash
root@debian:/home/toor# lvcreate -n lv01 vg-01 -L 10G
WARNING: ext4 signature detected on /dev/vg-01/lv01 at offset 1080. Wipe it? [y/n]: y
  Wiping ext4 signature on /dev/vg-01/lv01.
  Logical volume "lv01" created.

root@debian:/home/toor# vgs
  VG        #PV #LV #SN Attr   VSize   VFree
  debian-vg   1   5   0 wz--n- <19.52g    0
  vg-01       2   1   0 wz--n-  15.99g **5.99g**

root@debian:/home/toor# lvcreate -n lv02 vg-01 -L 5.99G
  Rounding up size to full physical extent 5.99 GiB
WARNING: ext4 signature detected on /dev/vg-01/lv02 at offset 1080. Wipe it? [y/n]: y
  Wiping ext4 signature on /dev/vg-01/lv02.
  Logical volume "lv02" created.

root@debian:/home/toor# lvdisplay
  --- Logical volume ---
  LV Path                **/dev/vg-01/lv01**
  LV Name                lv01
  VG Name                vg-01
  LV UUID                6srexE-r1e3-CrF8-M8Y7-NEq5-enRO-WWh71S
  LV Write Access        read/write
  LV Creation host, time debian, 2021-10-09 08:29:53 -0400
  LV Status              available
  # open                 1
  LV Size                10.00 GiB
  Current LE             2560
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           254:5

  --- Logical volume ---
  LV Path                **/dev/vg-01/lv02**
  LV Name                lv02
  VG Name                vg-01
  LV UUID                XtKanF-3ZPX-8hcz-6j37-qwAL-SGCb-Cg9gdc
  LV Write Access        read/write
  LV Creation host, time debian, 2021-10-09 08:37:19 -0400
  LV Status              available
  # open                 0
  LV Size                5.99 GiB
  Current LE             1534
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           254:6

root@debian:/home/toor# mkfs.ext4  /dev/vg-01/lv01
root@debian:/home/toor# mkfs.ext4  /dev/vg-01/lv02

root@debian:/home/toor# lsblk
NAME                  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                     8:0    0   20G  0 disk
├─sda1                  8:1    0  487M  0 part /boot
├─sda2                  8:2    0    1K  0 part
└─sda5                  8:5    0 19.5G  0 part
  ├─debian--vg-root   254:0    0    4G  0 lvm  /
  ├─debian--vg-var    254:1    0  1.7G  0 lvm  /var
  ├─debian--vg-swap_1 254:2    0  976M  0 lvm  [SWAP]
  ├─debian--vg-tmp    254:3    0  364M  0 lvm  /tmp
  └─debian--vg-home   254:4    0 12.5G  0 lvm  /home
sdb                     8:16   0    8G  0 disk
└─vg--01-lv01         254:5    0   10G  0 lvm  /mnt
sdc                     8:32   0    8G  0 disk
├─vg--01-lv01         254:5    0   10G  0 lvm  /mnt
└─vg--01-lv02         254:6    0    6G  0 lvm
sdd                     8:48   0    9G  0 disk
sr0                    11:0    1 1024M  0 rom
```

```bash
root@debian:/home/toor# pvcreate /dev/sdd
  Physical volume "/dev/sdd" successfully created.

root@debian:/home/toor# pvs
  PV         VG        Fmt  Attr PSize   PFree
  /dev/sda5  debian-vg lvm2 a--  <19.52g     0
  /dev/sdb   vg-01     lvm2 a--   <8.00g <8.00g
  /dev/sdc   vg-01     lvm2 a--   <8.00g  2.00g
  /dev/sdd             lvm2 ---    9.00g  9.00g

root@debian:/home/toor# vgs
  VG        #PV #LV #SN Attr   VSize   VFree
  debian-vg   1   5   0 wz--n- <19.52g     0
  vg-01       2   1   0 wz--n-  15.99g 10.00g

root@debian:/home/toor# vgextend vg-01 /dev/sdd
  Volume group "vg-01" successfully extended

root@debian:/home/toor# lvextend /dev/mapper/vg--01-lv02 -L +5G
  Size of logical volume vg-01/lv02 changed from 5.99 GiB (1534 extents) to 10.99 GiB (2814 extents).
  Logical volume vg-01/lv02 successfully resized.

root@debian:/home/toor# mount /dev/mapper/vg--01-lv02 /mnt
root@debian:/home/toor# df -h
Filesystem                   Size  Used Avail Use% Mounted on
udev                         963M     0  963M   0% /dev
tmpfs                        196M  572K  196M   1% /run
/dev/mapper/debian--vg-root  3.9G  794M  2.9G  22% /
tmpfs                        980M     0  980M   0% /dev/shm
tmpfs                        5.0M     0  5.0M   0% /run/lock
/dev/mapper/debian--vg-tmp   343M   12K  321M   1% /tmp
/dev/mapper/debian--vg-var   1.6G  240M  1.3G  16% /var
/dev/mapper/debian--vg-home   13G   64K   12G   1% /home
/dev/sda1                    470M   48M  398M  11% /boot
tmpfs                        196M     0  196M   0% /run/user/1000
**/dev/mapper/vg--01-lv02      4.9G   24K  4.6G   1% /mnt**

root@debian:/home/toor# resize2fs /dev/mapper/vg--01-lv02
resize2fs 1.46.2 (28-Feb-2021)
Filesystem at /dev/mapper/vg--01-lv02 is mounted on /mnt; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 2
The filesystem on /dev/mapper/vg--01-lv02 is now 2621440 (4k) blocks long.

root@debian:/home/toor# df -h
Filesystem                   Size  Used Avail Use% Mounted on
udev                         963M     0  963M   0% /dev
tmpfs                        196M  572K  196M   1% /run
/dev/mapper/debian--vg-root  3.9G  794M  2.9G  22% /
tmpfs                        980M     0  980M   0% /dev/shm
tmpfs                        5.0M     0  5.0M   0% /run/lock
/dev/mapper/debian--vg-tmp   343M   12K  321M   1% /tmp
/dev/mapper/debian--vg-var   1.6G  240M  1.3G  16% /var
/dev/mapper/debian--vg-home   13G   64K   12G   1% /home
/dev/sda1                    470M   48M  398M  11% /boot
tmpfs                        196M     0  196M   0% /run/user/1000
**/dev/mapper/vg--01-lv02      9.8G   23M  9.3G   1% /mnt**
```