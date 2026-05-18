# BUILDING OS FROM SCRATCH

# DAY #0 — Building an Empty Bootable OS

This project marks the beginning of a custom operating system development journey using low-level x86 assembly programming.

The objective of Day #0 is simple:

- create a valid bootable binary
- understand BIOS boot requirements
- generate a floppy disk image
- boot it using QEMU

At this stage, the operating system does not perform any useful task.  
It only boots successfully and halts the CPU safely.

---

# Development Environment

| Tool | Purpose |
|---|---|
| NASM | Assembler |
| QEMU | Hardware Emulator |
| Make | Build Automation |
| x86 Assembly | Low-Level Programming |

---

# Repository Structure

```text
.
|-- README.md
|-- build
|   |-- main.bin
|   `-- main_floppy.img
|-- images
|   `-- total execution.png
|-- makefile
`-- src
    `-- main.asm
```

---

# Source Code

## `src/main.asm`

```asm
org 0x7C00
bits 16

main:
    hlt

.halt:
    jmp .halt

times 510-($-$$) db 0
dw 0xAA55
```

---

# Makefile

## `makefile`

```make
ASM=nasm

SRC_DIR=src
BUILD_DIR=build

$(BUILD_DIR)/main_floppy.img: $(BUILD_DIR)/main.bin
	cp $(BUILD_DIR)/main.bin $(BUILD_DIR)/main_floppy.img
	truncate -s 1440k $(BUILD_DIR)/main_floppy.img

$(BUILD_DIR)/main.bin: $(SRC_DIR)/main.asm
	$(ASM) $(SRC_DIR)/main.asm -f bin -o $(BUILD_DIR)/main.bin
```

---

# Building the OS

Compile the boot sector:

```bash
make
```

---

# Running the OS

Boot the floppy image using QEMU:

```bash
qemu-system-x86_64 -fda ./build/main_floppy.img
```

---

# Execution Output

![Execution Output](images/total%20execution.png)

---

# Understanding the Bootloader

---

## `org 0x7C00`

```asm
org 0x7C00
```

The BIOS loads the boot sector into memory address:

```text
0x7C00
```

This directive tells NASM where the code will exist in memory so that labels and addresses are calculated correctly.

---

## `bits 16`

```asm
bits 16
```

x86 systems begin execution in:

```text
16-bit Real Mode
```

This directive forces NASM to generate 16-bit instructions compatible with BIOS startup mode.

---

## `hlt`

```asm
hlt
```

Stops CPU execution until the next hardware interrupt occurs.

---

## Infinite Halt Loop

```asm
.halt:
    jmp .halt
```

If the CPU wakes up after `hlt`, execution enters an infinite loop.

This prevents the processor from executing random memory data.

---

## Boot Sector Padding

```asm
times 510-($-$$) db 0
```

A BIOS boot sector must be exactly:

```text
512 bytes
```

This directive fills unused space with zeros until byte 510.

---

## Boot Signature

```asm
dw 0xAA55
```

The final two bytes of a valid boot sector must contain:

```text
0x55AA
```

Without this signature:
- BIOS assumes the disk is not bootable
- execution is skipped

---

# Why Must the Binary Be 512 Bytes?

The BIOS reads exactly one sector from the boot device.

Standard sector size:

```text
512 bytes
```

Therefore:
- smaller binaries may miss the boot signature
- larger binaries are truncated during loading

The entire bootloader must fit within one sector.

---

# Why Use `0xAA55`?

`0xAA55` is the standard x86 BIOS boot signature.

The BIOS checks:
- byte 510 = `0x55`
- byte 511 = `0xAA`

If the signature is not present:
- BIOS treats the device as non-bootable

This convention is part of legacy IBM PC architecture.

---

# Why Create a 1.44MB Floppy Image?

The floppy image is used because:
- BIOS directly supports floppy booting
- floppy geometry is simple
- QEMU automatically recognizes standard floppy sizes

Standard floppy size:

```text
80 tracks × 2 heads × 18 sectors × 512 bytes
= 1,474,560 bytes
= 1440 KB
```

The command:

```bash
truncate -s 1440k
```

pads the boot sector into a complete floppy disk image.

---

# Build Process

The complete workflow:

```text
Assembly Source (.asm)
        ↓
Flat Binary (.bin)
        ↓
Floppy Disk Image (.img)
        ↓
QEMU Emulation
```

---

# Important Commands

## Build

```bash
make
```

## Run

```bash
qemu-system-x86_64 -fda ./build/main_floppy.img
```

---

# Learning Objectives

This stage introduces:

- BIOS boot process
- x86 Real Mode
- Boot sector structure
- Flat binary generation
- Boot signatures
- Floppy image creation
- Low-level memory addressing
- Hardware emulation using QEMU

---

# Status

## Completed

- bootable binary creation
- BIOS-compatible boot sector
- floppy image generation
- QEMU execution

## Next Steps

- printing text to screen
- BIOS interrupts
- keyboard interaction
- protected mode transition
- kernel initialization

---

# License

This project is intended for educational and research purposes.
