# Day 01 - Stage 1 Bootloader

This folder contains a basic **x86 16-bit bootloader** built and tested using **QEMU**.

The bootloader is written in NASM assembly and converted into a raw binary boot sector. The binary is then placed inside a floppy disk image and executed through QEMU.

---

## Folder Structure

```text
.
|-- build
|   |-- main.bin
|   `-- main_floppy.img
|-- makefile
`-- src
    `-- main.asm
```

---

## Files

| File | Description |
|---|---|
| `src/main.asm` | 16-bit bootloader source code |
| `makefile` | Build automation file |
| `build/main.bin` | Raw bootloader binary |
| `build/main_floppy.img` | Bootable floppy image used by QEMU |

---

## Current Implementation

This bootloader:

- Runs in **16-bit real mode**
- Is loaded by BIOS at memory address `0x7C00`
- Uses a **512-byte boot sector**
- Contains the boot signature `0xAA55`
- Boots through a floppy image in QEMU

---

## Boot Process

```text
BIOS
  ↓
Loads boot sector into 0x7C00
  ↓
Executes bootloader code
  ↓
Boots from floppy image
```

---

## Build and Run

Build the bootloader:

```bash
make
```

Run the floppy image in QEMU:

```bash
qemu-system-x86_64 -fda ./build/main_floppy.img
```

---

## Output

QEMU detects the floppy image and starts the boot process.

```text
Booting from Hard Disk...
Boot failed: could not read the boot disk

Booting from Floppy...
```

![QEMU Boot Output](images/os%20does%20nothing.png)

---

## Notes

- The boot sector must be exactly **512 bytes**.
- The boot signature must be placed at the end of the sector.
- `0xAA55` is required for BIOS to recognize the sector as bootable.
- The current bootloader does not print text or load any external program.
