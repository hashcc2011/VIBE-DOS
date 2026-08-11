# VIBE-DOS
**VIBE-DOS** is a custom, lightweight bare-metal 16-bit operating system built entirely from scratch in C. It does not run on top of Linux, Windows, or DOSBox AT ALL, writing directly to VGA memory and communicating directly with x86 hardware ports.

<img width="732" height="480" alt="image" src="https://github.com/user-attachments/assets/0b0adba6-94fe-4f45-bf8d-e814cce625fa" />
<img width="737" height="475" alt="image" src="https://github.com/user-attachments/assets/781a8dec-fa6d-47c0-a648-28e796d54b70" />
<img width="727" height="477" alt="image" src="https://github.com/user-attachments/assets/adc19623-a830-4ea8-8ebb-ea1e03485682" />

Oh, and it uses a custom serial bridge to talk to Gemini 3.6 Flash over a 1990s dumb-terminal interface. This was an incredibly stupid thing to program, but it was worth it.

## DISCLAMIER
This is a passion project and a hobbyist OS. It writes raw data to ATA ports. Run this inside the provided QEMU emulator and DO NOT attempt to boot this on your daily-driver physical hardware UNDER ANY CIRCUMSTANCES. This could corrupt your hard drive.
## Features
* **Live AI Serial Bridge (`chat`):** A custom hardware interrupt loop on COM1 (`0x3F8`) that connects the bare-metal OS to a modern Python client on the host machine, allowing two-way communication with the Gemini API. 
* **vEdit Word Processor (`edit`):** A classic MS-DOS style graphical text editor featuring ATA hardware saving directly to the VIBE-FAT disk cache.
* **vSheets (`sheets`):** A hardware-accelerated, grid-based spreadsheet application supporting 16 rows, 4 columns, real-time recalculation, and column summation. This is a heavy WIP.
* **VIBE-BASIC Interpreter (`basic`):** A fully functional BASIC interpreter capable of executing `.BAS` files with support for `PRINT`, `INPUT`, `LET`, `IF/GOTO`, `BEEP`, `COLOR`, and `DELAY`.
* **VIBE-FAT File System:** A custom ATA PIO Hard Drive driver with a built-in disk cache, supporting 2KB files and dynamic sector writing.
* **Batch Scripting (`batch`):** Reads text files and executes lines sequentially (automatically runs `STARTUP.BAT` on boot).
* **Hardware Matrix Rain (`matrix`):** Because every custom OS needs a hardware-accelerated PRNG digital rain effect.

## How to Run
Get this - you don't need to compile it! I've made a .bat file to make it easy.

**IMPORTANT: YOU NEED QEMU INSTALLED TO RUN THIS. IF YOU DO NOT HAVE QEMU, YOU WILL NOT BE ABLE TO RUN THIS.**

1. Go to the **[Releases](../../)** tab and download the latest .zip file.
2. Extract the folder to your desktop.
3. Double-click `Run_VIBEDOS.bat`.
4. The bridge will open and ask for your free [Google Gemini API Key](https://aistudio.google.com/). Paste it in and hit Enter.
5. QEMU will boot the OS automatically!
Once you are at the `C:\>` prompt, type `help` to see all commands, or type `chat` to establish the AI serial link!

## How It Works
VIBE-DOS is a monolithic kernel built without standard libraries. 

* **VGA Text Mode (`0xB8000`):** All UI elements (vEDIT, vSHEETS) are drawn by calculating direct offsets in video memory.
* **Keyboard Drivers (`0x60` / `0x64`):** Custom scancode-to-ASCII translation mapping, including Shift/Caps-Lock state tracking and local line-buffering.

* **CMOS RTC (`0x70` / `0x71`):** Custom BCD-to-Binary translation to pull real-time hardware clock data. 

