# Day 01 - Stage 1 Bootloader

This folder contains a basic **x86 16-bit stage 1 bootloader** built using **NASM** and tested using **QEMU**.

The bootloader is assembled into a raw binary, copied into a floppy disk image, and executed as a bootable image.

---

## Folder Structure

```text
.
|-- README.md
|-- build
|   |-- main.bin
|   `-- main_floppy.img
|-- images
|   `-- Screenshot 2026-05-26 210814.png
|-- makefile
`-- src
    `-- main.asm
```

---

## Files

| File | Description |
|---|---|
| `src/main.asm` | Main 16-bit bootloader source code |
| `makefile` | Build and run automation |
| `build/main.bin` | Raw boot sector binary |
| `build/main_floppy.img` | Bootable floppy disk image |
| `images/Screenshot 2026-05-26 210814.png` | QEMU execution screenshot |

---

## Current Implementation

This bootloader:

- Runs in **16-bit real mode**
- Starts from BIOS-loaded address `0x7C00`
- Initializes segment registers
- Sets up the stack
- Uses BIOS video interrupt `int 0x10`
- Prints a text message on the QEMU screen
- Ends with a halt loop
- Contains the boot signature `0xAA55`

---

## Build

```bash
make
```

This generates:

```text
build/main.bin
build/main_floppy.img
```

---

## Run

```bash
qemu-system-x86_64 -fda ./build/main_floppy.img
```

---

## Output

The bootloader runs successfully in QEMU and prints:

```text
I am Narendaran, exploring OS development
```

![QEMU Output](images/Screenshot%202026-05-26%20210814.png)

---

## Key Concepts Used

| Concept | Purpose |
|---|---|
| `org 0x7C00` | Matches the BIOS bootloader load address |
| `bits 16` | Generates 16-bit real mode instructions |
| Segment setup | Initializes memory access through segment registers |
| Stack setup | Provides stack space for calls and register saving |
| `int 0x10` | BIOS video interrupt used for text output |
| `0xAA55` | Boot signature required by BIOS |

---

## Summary

This stage creates a working boot sector that can be loaded by BIOS, executed in QEMU, and used to print text directly through BIOS services.
