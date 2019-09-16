
http://3zanders.co.uk/2017/10/13/writing-a-bootloader/

BIOS interrupt calls are a facility that operating systems and application programs use to invoke the facilities of the Basic Input/Output System on IBM PC compatible computers. Traditionally, BIOS calls are mainly used by DOS programs and some other software such as boot loaders (including, mostly historically, relatively simple application software that boots directly and runs without an operating system—especially game software). (https://en.wikipedia.org/wiki/BIOS_interrupt_call)

The Global Descriptor Table (GDT) is a data structure used by Intel x86-family processors starting with the 80286 in order to define the characteristics of the various memory areas used during program execution, including the base address, the size, and access privileges like executability and writability. These memory areas are called segments in Intel terminology. (https://en.wikipedia.org/wiki/Global_Descriptor_Table)

Here’s what the fields in the GDT table mean:

- base a 32 bit value describing where the segment begins
- limit a 20 bit value describing where the segment ends, can be multiplied by 4096 if granularity = 1
- present must be 1 for the entry to be valid
- ring level an int between 0-3 indicating the kernel Ring Level
- direction
-   0 = segment grows up from base, 1 = segment grows down for a data segment
-   0 = can only execute from ring level, 1 = prevent jumping to higher ring levels
- read/write if you can read/write to this segment
- accessed if the CPU has accessed this segment
- granularity 0 = limit is in 1 byte blocks, 1 = limit is multiples of 4KB blocks
- size 0 = 16 bit mode, 1 = 32 bit protected mode

