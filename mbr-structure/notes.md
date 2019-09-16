# MBR Structure
- Partition Table: A disk partition is a logical division of the disk, into which a file system can be created in order to install an operating system (such as Windows or Linux), or store various types of files.�The partition table effectively retains the particular details for each primary partition on the disk, such as starting position, size, type, status, etc.�A standard MBR reserves space for up to four partitions, although only one is necessary for proper operation of the computer.

- Boot Loader: Most of the first 446 bytes of the disk are dedicated to telling the computer how to boot.�When a machine first starts it needs to locate the necessary operating system files on the hard disk, so it turns to the boot loader for that information.�The boot loader is actually a small program which identifies the active (bootable) partition, then redirects the boot process to that location.�MBRWizard is able to repair the boot loader in case it gets overwritten or corrupted.

- Disk Signature: Located at byte 440, this is simply a unique identifier for the disk.�This is typically used by Windows to remember the assigned drive letters for each partition, but is also used by various operating systems to identify the correct boot volume.

- Magic Number: Located in the final two bytes of the MBR (511-512), this section must contain the hex value AA55, which officially classifies this as a valid MBR. An invalid magic number indicates a corrupt or missing MBR, therefore these bytes are critical to booting or using the disk.

Source: http://mbrwizard.com/thembr.php

See also: https://github.com/Georgantas/linux-kernel-module-experiments/blob/master/block-devices/partition.c
