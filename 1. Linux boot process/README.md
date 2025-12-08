# Linux boot process

## 1. BIOS
- Basic Input/Output System
- BIOS software is located on a ROM chip on the motherboard
- Initializes screen, keyboard
- Performs integrity checks
- Tests main memory
- Searches for boot loader: floppy, CD, HDD
- Loads bootloader to memory and gives control to it

## 2. MBR
- Master Boot Record
- Located on the first sector ( /dev/hda  /dev/sda ) of the bootable disk
- or located in the EFI partition (in a UEFI system)
- CMOS values are loaded (date, time...)
- executes GRUB (or other) boot loader
- MBR size is 512 bytes

## 3. GRUB
- Grand Unified Bootloader
- /boot/grub/grub.conf
- loads kernel -> if there are multiple kernels you can choose one
- GRUB has knowledge of the filesystem

## 4. Kernel
- mounts root filesystem (specified in grub.conf)
- kernel is usually compressed -> uncompress first
- initrd = initial RAM diks
    - temporary filesystem until kernel is booted
- initialize any hardware drivers built into the kernel

## 5. Init
- kernel executes init -> /sbin/init
- since it was the first program to be executed -> PID=1
- looks at `/etc/inittab` -> default initlevel