# VIBE-DOS
**A 32-bit Protected Mode Operating System built from absolute scratch. No libraries, no premade bootloaders and stuff, everything is made from C.**

VIBE-DOS is a custom, bare-metal operating system written entirely in C and x86 Assembly. It bypasses legacy 16-bit BIOS interrupts in favor of a custom-built 32-bit kernel, featuring its own FAT16 file system driver, dynamic memory allocation, and a decoupled `int 0x21` system call architecture.

### Features
* **Custom Bootloader & Kernel:** Boots into a flat 32-bit memory model.
* **FAT16 Injection:** Reads and executes standalone `.BIN` applications dynamically from a virtual hard drive.
* **Visual Manager (`vNAV`):** A flawless, anti-scrolling, retro MS-DOS style GUI file explorer.
* **The App Suite:** Includes a standalone Word Processor (`vEDIT`), Spreadsheet (`vSHEETS`), and a functional BASIC interpreter.
* **Gaming & Art:** Features a 60-FPS Tetris clone (`TETRIS.BIN`) and a 16-color ANSI paint studio (`DRAW.BIN`).

---

### Prerequisites
To build and run VIBE-DOS, you must be in a Linux environment. If you are on Windows, you **must** use Windows Subsystem for Linux (WSL).

1. **WSL (Windows Subsystem for Linux):** Ubuntu recommended.
2. **Code Editor:** VS Code (with the WSL extension) or your editor of choice.
3. **Build Tools & Emulator:** Open your WSL terminal and install the required packages:
   ```bash
   sudo apt update
   sudo apt install gcc nasm qemu-system-x86 mtools dosfstools wget

## WARNING!
This is a hobby OS and is meant for virtual machines. **DO NOT RUN THIS ON REAL HARDWARE UNLESS YOU'RE RISKING TO CORRUPT YOUR HARD DRIVE!**
