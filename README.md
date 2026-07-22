# Compie-Linux
Compie linux - a simple systemd-free linux distribution.

Default Username: root

Default Password: compie

Basic install goes as such:

# partition disks
example:

using cfdisk or fdisk on your drive which can be found using lsblk

# mount partitions
example:

mount /dev/nvme0n1p3 /mnt/compie (assuming nvme0n1p3 is the root partition)

# extract base system tarball to root partition
example:

tar xpvf compiebase-*.tar.xz --xattrs-include='*.*' --numeric-owner -C /mnt/compie

# compile kernel
I highly recommend following the linux from scratch guide for this or the gentoo guide as they are extremely straightforward and better than what a single dev can create on a github readme
links for info:
https://www.linuxfromscratch.org/lfs/view/development/chapter10/kernel.html
the source code for the kernel to compile from can be obtained from kernel.org
example:

❯ wget https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.1.4.tar.xz

--2026-07-22 01:13:39--  https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.1.4.tar.xz
Loaded CA certificate '/etc/ssl/certs/ca-certificates.crt'
Resolving cdn.kernel.org (cdn.kernel.org)... 2a04:4e42:2e::432, 151.101.197.176
Connecting to cdn.kernel.org (cdn.kernel.org)|2a04:4e42:2e::432|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 158290768 (151M) [application/x-xz]
Saving to: ‘linux-7.1.4.tar.xz’

linux-7.1.4.tar.xz           100%[==============================================>] 150.96M  13.3MB/s    in 9.6s    

2026-07-22 01:13:49 (15.8 MB/s) - ‘linux-7.1.4.tar.xz’ saved [158290768/158290768]

# configure the bootloader
very straightforward process, grub is built into the system but if you prefer another bootloader such as limine consider installing it from source using the built in package manager or BLFS handbook
example:

grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=CompieLinux

grub-mkconfig -o /boot/grub/grub.cfg
