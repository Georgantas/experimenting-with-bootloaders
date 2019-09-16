
https://wiki.osdev.org/Rolling_Your_Own_Bootloader

BIOS (Basic Input/Output System) was created to offer generalized low-level services to early PC system programmers. The basic aims were: to hide (as much as possible) variations in PC models and hardware from the OS and applications, and to make OS and application development easier (because the BIOS services handled most of the hardware level interface). These BIOS services are still used (especially during bootup), and are often named "BIOS functions". In Real Mode, they can be easily accessed through software interrupts, using Assembly language. (https://wiki.osdev.org/BIOS)

Real Mode is a simplistic 16-bit mode that is present on all x86 processors. Real Mode was the first x86 mode design and was used by many early operating systems before the birth of Protected Mode. For compatibility purposes, all x86 processors begin execution in Real Mode. (https://wiki.osdev.org/Real_Mode)

Since the bootloader runs in Real Mode, it has easier access to BIOS resources and functions. Therefore it's a good place to perform memory map detection, detecting available video modes, loading additional files etc. The bootloader will collect this information and present it in a way the kernel will be able to understand.

Bootloader good place to do:
    - Memory map detection: One of the most vital pieces of information that an OS needs in order to initialize itself is a map of the available RAM on a machine. Fundamentally, the best way an OS can get that information is by using the BIOS. There may be rare machines where you have no other choice but to try to detect memory yourself -- however, doing so is unwise in any other situation. (https://wiki.osdev.org/How_Do_I_Determine_The_Amount_Of_RAM)
    - Detecting available video modes: (https://wiki.osdev.org/Getting_VBE_Mode_Info)
    - Loading additional files, etc.
    - Enabling A20: The A20 Address Line is the physical representation of the 21st bit (number 20, counting from 0) of any memory access. When the IBM-AT (Intel 286) was introduced, it was able to access up to sixteen megabytes of memory (instead of the 1 MByte of the 8086). But to remain compatible with the 8086, a quirk in the 8086 architecture (memory wraparound) had to be duplicated in the AT. To achieve this, the A20 line on the address bus was disabled by default. (https://wiki.osdev.org/A20)
    - Entering protected mode

Once data the above information is obtained, organize it in a flat table (see BIOS data area: https://wiki.osdev.org/BIOS).

To get info about all the generic and manufacturer specific Real Mode BIOS interrupt calls on x86, see Ralf Brown's interrupt list: https://wiki.osdev.org/Ralf_Brown%27s_Interrupt_List (exhaustive list of interrupt functions).

The contents of memory just before the bootloader runs: https://wiki.osdev.org/Memory_Map_(x86)


