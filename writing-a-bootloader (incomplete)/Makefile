
all:
	nasm -f bin boot1.asm -o boot1.bin

read:
	hexdump boot1.bin

# run qemu and boot from floppy
boot:
	qemu-system-x86_64 -fda boot1.bin

