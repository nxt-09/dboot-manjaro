# dual-boot-arch

## System Info
- **Firmware Interface** = UEFI
- **Architecture** = 64-bit
-  **Manufacturer** - Asus
-  **HDD** = 431 GB
-  **RAM** = 8 GB
-  **OS0** = Win10
-  **OS1** = Manjaro KDE

## Check UEFI or BIOS [Legacy]
-  Run **`msinfo32`**
-  BIOS Mode = EFI or UEFI, not Legacy

## Create Bootable USB
- Get [Rufus](https://rufus.ie/)
- Select GPT+UEFI if possible
- Start and remove USB after done.

## Create Disk Partition
- Run **`diskmgmt.msc`**
- Shrink necessary drives
- Leave the unallocated space

## Disable Fast Startup
Control Panel ➤ Hardware and Sound ➤ Power Options ➤ Choose what the power buttons do ➤ Turn on fast startup box [Uncheck]

## Disable Secureboot
Settings ➤ Update ➤ Recovery ➤ Advanced ➤ Restart ➤ Troubleshoot ➤ Advanced ➤ UEFI ➤ Restart ➤ Security ➤ Secure Boot [Disable] ➤ Save & Exit

## Installation
Boot USB with UEFI ➤ Connect Internet ➤ Launch Installer ➤ Manual partitioning

#### Partitions

||Size [MB]|Filesystem|Mountpoint|Flags|
| :------------ | :------------ | :------------ | :------------ | :------------ |
|**EFI**|512|FAT32|/boot/efi|boot|
|**Swap**|10240|linuxswap|-|-|
|**Root**|40960|ext4|/|-|
|**Home**|Rest|ext4|/home|-|

## GRUB
#### Verify Boot Rank
- Do not Reboot
- Remove USB
- Open Terminal
- Enter **`efibootmgr`**

#### Open Windows
- Open BIOS on restart
- Select Windows Boot Manager
- Quickly select Windows from Linux GRUB

#### Install GRUB
- Run CMD as administrator
- Enter **`bcdedit /set {bootmgr} path \EFI\manjaro\grubx64.efi`**
- Reboot

## Restore USB
- Run CMD as administrator
- Enter **`diskpart`**
- Enter **`list disk`**
- Enter **`select disk x`** [x = disk number of USB drive]
- Enter **`clean`**
- Enter **`create partition primary`**
- Enter **`active`**
- Enter **`format fs=fat32 quick`**
- Enter **`exit`**
