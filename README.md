# proxmox-zfs 2.3.0-1

###### install dependencies:
```commandline
apt install build-essential autoconf libtool gawk alien fakeroot proxmox-headers-$(uname -r) pve-headers-$(uname -r) uuid-dev libblkid-dev zlib1g-dev libaio-dev libssl-dev libelf-dev python3 python3-dev python3-setuptools python3-cffi libffi-dev dkms
```

###### add repo:

```commandline
curl -s --compressed "https://meit-repo.github.io/proxmox-zfs/KEY.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/my_ppa.gpg >/dev/null
curl -s --compressed -o /etc/apt/sources.list.d/my_list_file.list "https://meit-repo.github.io/proxmox-zfs/my_list_file.list"
apt update
```

###### installation:
```commandline
apt install      zfs libzfs6 libnvpair3 libuutil3 libzfs6-devel libzpool6 pam-zfs-key zfs-dracut zfs-dkms zfs-initramfs
update-initramfs -u
```

###### do verification before reboot
```commandline
/usr/sbin/zfs --version|head -n 1
--- zfs-2.3.0-1
```

unzip initrd image and check in chroot
```commandline
rm -rf ~/verify_initrd
mkdir ~/verify_initrd
cd ~/verify_initrd/  
zstd -d -c /boot/initrd.img-$(uname -r) | cpio -id

chroot . /usr/bin/sh
zfs --version 2>null
--- zfs-2.3.0-1
modinfo /usr/lib/modules/$(uname -r)/updates/dkms/zfs.ko | grep ^version
--- 2.3.0-1
```

###### reboot:
reboot ...


###### verify after reboot
```commandline
/usr/sbin/zfs --version
--- zfs-2.3.0-1
--- zfs-kmod-2.3.0-1
```

###### ref:
https://assafmo.github.io/2019/05/02/ppa-repo-hosted-on-github.html
