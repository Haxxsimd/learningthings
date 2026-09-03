# learningthings
some useful stuff for things i wanna learn about

---

Based on the Awesome-Embedded repo and your background (soldering veteran, PC-building pro, new to embedded coding), here's a curated learning path split into the areas you mentioned.

---

## 🛠️ Microcontrollers & Embedded Programming

You already have an ST-LINK and have played with an e-scooter display – likely an STM32.

| Resource | Why it fits you | Level |
|----------|-----------------|-------|
| McuOnEclipse (STM32, STM8, ESP32 sections) | Walk-throughs of bare-metal projects using the same ST-LINK you already own. Very hands-on, starts with "hello world"s and builds up to peripheral drivers. | All levels |
| Bare-metal programming guide (listed in the repo) | A concise guide made for beginners – exactly your starting point. Covers registers, CMSIS, and getting code onto the chip without an IDE. | Beginner |
| Modern Embedded Systems Programming Course | Goes from basics to "modern practice" (defensive coding, memory-mapped I/O, etc.). Good bridge from "PC programmer" to "embedded developer". | Beginner–Intermediate |
| Valvano – "Embedded Systems – Shape The World" (TM4C123/ARM) | Classic university-level course, but the concepts transfer directly to any ARM-MCU (including STM32). Lab exercises use Code Composer Studio, but you can adapt to ST-LINK + GCC. | Intermediate |
| "Programming Embedded Systems" (Mike McCarthy) – free chapters online | Old-but-gold book. Explains the mindset of embedded C, bit-bashing, and dealing with limited resources. | Beginner |

**Quick start workflow you can use today:**
1. Download a STM32 "basic-template" project (the repo lists stm32f0-discovery-basic-template).
2. Open it in VS Code with the PlatformIO extension (no need for the official IDE).
3. Connect your ST-LINK, hit "Upload", and watch the LED blink.
4. Modify the GPIO pin to control the e-scooter display's debug pins you already probed.

---

## 📐 PCB Design

The repo only mentions KiCad in passing, but it's the natural next step after wiring up breadboards.

| Resource | Why it fits you | Level |
|----------|-----------------|-------|
| KiCad 7 Essential Training (Udemy / free YouTube series) | KiCad is free, open-source, and runs on Linux/Windows/macOS. Learn to draw schematics, make footprints, route 2-layer boards – perfect for your "look inside PCBs" curiosity. | Beginner |
| "Designing with KiCad" (Pragmatic Bookshelf) | Step-by-step book that walks a complete board from concept to Gerber files. Good if you learn better from a physical book. | Beginner–Intermediate |
| EEVblog "KiCad vs. Eagle" videos | Quick sanity-check on whether KiCad meets your workflow. | Beginner |
| OpenHardware.io (community projects) | Download real open-source boards, study their schematics, and trace how experienced designers lay out power sections, keep-out zones, etc. | Intermediate–Advanced |

**Your advantage:** You already understand trace current, via stitching, and clearance rules from building PCs. KiCad's "3D Viewer" will let you inspect your first boards in a way that feels natural.

---

## 🌿 Arduino & Raspberry Pi

Both are great "prototyping sandboxes" before you go full bare-metal.

| Resource | Why it fits you | Level |
|----------|-----------------|-------|
| Arduino Project Hub (project-based) | Search "STM32 Arduino" or "ESP32 Arduino" – many hobbyists use their ST-LINK to program Arduinos via a bootloader, good for quick wins. | Beginner |
| "Arduino Cookbook" (Michael Margolis) | Recipe-style book. If you already "get" C syntax, this jumps you straight to using shields, interrupts, and communicating with external ICs. | Beginner–Intermediate |
| "Exploring Raspberry Pi: Interfacing to the Real World with Embedded Linux" (Derek Molloy) | The gold standard for moving from "PC user" to "Pi tinkerer". Covers GPIO, PWM, I²C/SPI, and even bare-metal kernel modules if you get curious later. | Intermediate |
| Raspberry Pi Foundation's official tutorials | Free, browser-based, no install needed. Start with "Blink an LED", then "Read a sensor", then "Write Python to talk to your ST-LINK-debugged firmware". | Beginner |

**Suggestion:** Start with Arduino to practice C syntax and digital/analog I/O without worrying about OS layers. Move to Raspberry Pi when you want to add Linux, networking, and higher-level Python abstractions.

---

## 💻 Learning to Code (Embedded C)

You're a rookie at coding but a veteran at hardware – here's how to cross that bridge.

1. **Learn C the hard way** – start with a free online book like "C Programming Absolute Beginner's Guide" or "Learn C the Hard Way". Focus on pointers, arrays, and memory – these map 1:1 to embedded concepts like DMA and register manipulation.

2. **Practice on your PC first** – write a few C programs that manipulate an array or a struct, then compile with gcc. The edit-compile-run cycle is identical to embedded (just without the chip).

3. **Use a "debugger-simulator"** – tools like OpenOCD + GDB (both free) let you step through code on the STM32 without touching the board until you're ready. The repo's "Building Bare-Metal ARM Systems with GNU Tools" guide covers this.

4. **Read the datasheet like a story** – STM32 reference manuals are dense, but the "Getting Started with STM32" sections are essentially "here's how you blink an LED in C". Print the pinout, highlight it, and keep it on your desk.

---

## 🔧 Hardware Repair / Reverse-Engineering

You already love taking things apart – a few focused resources will sharpen that skill.

| Resource | Why it fits you | Level |
|----------|-----------------|-------|
| EEVblog "circuit repair" YouTube playlist | Real-world failure analysis, component-level diagnostics, and how to use an oscilloscope, multimeter, and yes, your ST-LINK, to read firmware from a broken board. | All levels |
| "BlackFlag ECU" (mentioned in the repo) | Focuses on CAN-bus security & protocol reverse-engineering – perfect if you ever want to dig into e-scooter or vehicle electronics. | Intermediate |
| "Hacking Electronics" (Simon Monk) | Bits-and-pieces on desoldering, probing, and repurposing hardware. Very hands-on. | Beginner |
| r/electronics & r/hardware (Reddit) | Community troubleshooting – post a teardown photo, get suggestions on likely failure points (capacitors, voltage regulators, etc.). | Ongoing |

**Pro tip:** After you extract a firmware dump with your ST-LINK, load it into Ghidra (NSA's free reverse-engineering tool) and try to make sense of the functions. Even if you can't decompile everything, seeing the memory map and interrupt vectors will reinforce your embedded C learning.

---

## 📚 Suggested Learning Sequence (your first 3–6 months)

| Month | Goal | Concrete steps |
|-------|------|-----------------|
| 1 | "Hello world" on an STM32 with your ST-LINK | → Install VS Code + PlatformIO → Pick a basic-template → Blink an LED → Read the pinout of your e-scooter display and probe a few nets |
| 2 | Understand registers & bare-metal GPIO | → Follow McuOnEclipse "GPIO tutorial" → Replace the LED with the display's control line → Write "set/clear" code without digitalWrite() |
| 3 | KiCad: draw your first schematic | → Watch a KiCad 7 intro series → Redraw the e-scooter display's power section on KiCad → Order a cheap 2-layer PCB (see PCBWay, JLCPCB prototyping) |
| 4 | Add a sensor or communication peripheral | → Hook up an I²C sensor (BME280, SSD1306 OLED) to the STM32 → Read the datasheet, write the init sequence → Log data to USB (via CDC or SPI) |
| 5 | Move to Raspberry Pi + Linux-level interfacing | → Flash a Raspberry Pi OS → Use Python to control GPIO → Read the "Exploring Raspberry Pi" chapter on PWM → Hook the Pi to your STM32 for "firmware-in-the-loop" testing |
| 6 | Small reverse-engineering project | → Take a broken consumer gadget, dump its firmware with the ST-LINK, try Ghidra → Identify a function that controls a LED or motor → Write a "companion" Arduino sketch that mimics it |

---

## 🛎️ Quick "start-now" checklist

- [ ] Install VS Code + PlatformIO (free, works with ST-LINK).
- [ ] Download an STM32 "basic-template" project (search the repo name stm32f0-discovery-basic-template or Google "STM32Cube firmware package").
- [ ] Connect your ST-LINK, press "Upload" in PlatformIO, and watch an LED blink.
- [ ] Open KiCad 7, follow a 1-hour YouTube "first schematic" tutorial, and redraw a simple section of a board you've taken apart.
- [ ] Read the first 3 chapters of "C Programming Absolute Beginner's Guide" (or watch a "C for complete beginners" playlist on YouTube).

From there, the path widens into RTOSes (FreeRTOS, Zephyr), motor-control firmware, or even designing your own custom PCB shields. The combination of your soldering chops and PC-building intuition is a huge head start.

**Happy hacking – and welcome to the embedded world! 🚀**
