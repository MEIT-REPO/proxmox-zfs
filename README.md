# proxmox-zfs 2.3 RC 2/3 ...

ref:

https://assafmo.github.io/2019/05/02/ppa-repo-hosted-on-github.html

install dependencies:

apt install build-essential autoconf libtool gawk alien fakeroot proxmox-headers-$(uname -r) pve-headers-$(uname -r) uuid-dev libblkid-dev zlib1g-dev libaio-dev libssl-dev libelf-dev python3 python3-dev python3-setuptools python3-cffi libffi-dev dkms

add repo:

curl -s --compressed "https://meit-repo.github.io/proxmox-zfs/KEY.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/my_ppa.gpg >/dev/null

curl -s --compressed -o /etc/apt/sources.list.d/my_list_file.list "https://meit-repo.github.io/proxmox-zfs/my_list_file.list"

apt update

add zfs-2.3:

apt install zfs-dkms

update-initramfs -u

proxmox-boot-tool refresh

If you want to double confirm zfs.ko were installed correctly in initrd.img

mkdir ~/verify_initrd

cd ~/verify_initrd/

Use path of your initrd image to replace below /boot/initrd.img-6.8.4-2-pve

zstd -d -c /boot/initrd.img-6.8.4-2-pve | cpio -id

Verify version, it should be 2.3.0-rc2

find -name "zfs.ko" | xargs modinfo | head -n 2

Verify cksum of zfs.ko

find -name "zfs.ko" | xargs cksum # Verify output of zfs.ko

Output should be

2778772614 9588325 ./usr/lib/modules/6.8.4-2-pve/updates/dkms/zfs.ko

3243648977 9481837 ./usr/lib/modules/6.8.12-3-pve/updates/dkms/zfs.ko
