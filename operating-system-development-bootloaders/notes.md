
http://www.brokenthorn.com/Resources/OSDevIndex.html

https://www.intel.com/content/www/us/en/architecture-and-technology/64-ia-32-architectures-software-developer-vol-3a-part-1-manual.html

The BIOS boot stages: http://www.brokenthorn.com/Resources/OSDev3.html

The registers the x86 use for segment refrencing are as follows:

- CS (Code Segment) - Stores base segment address for code
- DS (Data Segment) - Stores base segment address for data
- ES (Extra Segment) - Stores base segment address for anything
- SS (Stack Segment) - Stores base segment address for the stack

There is some important things to remember about Protected Mode:

- Absolutley no interrupts will be avilable. You will need to write them yourself. The use of any interrupt--hardware or software will cause a Triple Fault
- Once you switch into pmode, the *slightest* mistake will cause a Triple Fault. Be carefull.
- PMode requires the use of Descriptor Tables, such as the GDT, LDT, and IDTs.
- PMode gives you access to 4 GB of Memory, With Memory Protection
- Segment:Offset Addressing is used along with Linear Addressing
- Access and use of 32 bit registers

General x86 Real Mode Memory Map:

- 0x00000000 - 0x000003FF - Real Mode Interrupt Vector Table
- 0x00000400 - 0x000004FF - BIOS Data Area
- 0x00000500 - 0x00007BFF - Unused
- 0x00007C00 - 0x00007DFF - Our Bootloader
- 0x00007E00 - 0x0009FFFF - Unused
- 0x000A0000 - 0x000BFFFF - Video RAM (VRAM) Memory. By writing bytes to this location, you effectivly change what is currently in video memory, and effectivly, what is displayed on screen. Modern graphics cards use GBs of this... gadamn
- 0x000B0000 - 0x000B7777 - Monochrome Video Memory
- 0x000B8000 - 0x000BFFFF - Color Video Memory
- 0x000C0000 - 0x000C7FFF - Video ROM BIOS
- 0x000C8000 - 0x000EFFFF - BIOS Shadow Area
- 0x000F0000 - 0x000FFFFF - System BIOS

Our Stage 2 bootloader, will do several things. It can:

- Enable and go into protected mode
- Retrieve BIOS information
- Load and execute the kernel
- Provide advance boot options (Such as Safe Mode, for example)
- Through configuration files, you can have KRNLDR boot from multiple operating system kernels
- Enable the 20th address line for access up to 4 GB of memory
- Provide basic interrupt handling

The 80x86 processor maps the memory regions based off the Global Descriptor Table (GDT). The processor will generate a General Protection Fault (GPF) exception if you do not follow the GDT. Because we have not set up interrupt handlers, this will result in a triple fault. Global Descriptor Table (GDT), Local Descriptor Table (LDT), and Interrupt Descriptor Table (IDT); each base address is stored in the GDTR, LDTR, and IDTR x86 processor registers.

In our current GDT, We have 2 descriptors: Each for Kernel Mode Ring 0. This is our Kernel Space.

All we need to do is to add 2 mode descriptors to our current GDT, but set for Ring 3 access. This is our User Space. 

Ways to switch modes:

- Interrupts: A Software Interrupt is a special type of interrupt implimented in software. Interrupts are used quite often, and rely on the use of a special table--the Interrupt Descriptor Table (IDT). We will look at Interrupts alot more closer later, as it is the first thing we will impliment in our Kernel. Linux uses INT 0x80 for all system calls.
- Call Gates: Call Gates provide a way for Ring 3 applications to execute more prividged (Ring 0,1,2) code.
- SYSENTER / SYSEXIT Instructions: These instructions were introduced from the Pentium II and later CPUs. Some recent AMD processors also support these instructions.

Hardware abstraction layer: A HAL is a software abstraction layer used to provide an interface to the physical hardware. It is an abstraction layer. These abstractions provide a way to interact with devices, while not needing to know the details of a particular device or controller. Normally in modern OSs, the HAL is a basic Motherboard chipset driver. It provides a basic interface between the kernel and the hardware of the machine, including the processor. This is great, as the Kernel can interact with the HAL whenever it needs access to the hardware. This also means that the kernel can be completely hardware independent. 


