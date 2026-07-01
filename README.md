# 🔌 Arduino EEPROM Programmer

<p align="center">
  <img src="schematic.png" alt="EEPROM Programmer Schematic" width="900">
</p>

<p align="center">

![Arduino](https://img.shields.io/badge/Arduino-Nano-00979D?style=for-the-badge&logo=arduino)
![Language](https://img.shields.io/badge/Language-C%2B%2B-blue?style=for-the-badge)
![EEPROM](https://img.shields.io/badge/EEPROM-28C16%20%7C%2028C64%20%7C%2028C256-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Arduino-orange?style=for-the-badge)

</p>

---

# 📖 Overview

The **Arduino EEPROM Programmer** is a hardware and software project designed to program parallel EEPROM chips such as the **28C16**, **28C64**, and **28C256** using an **Arduino Nano**.

Because an Arduino does not provide enough GPIO pins to directly control every address, data, and control line of these EEPROM chips, this project expands the available outputs using **two 74HC595 shift registers**.

Besides acting as a general EEPROM programmer, this project also contains additional sketches used to generate ROMs for an **8-bit breadboard computer**, including:

- Decimal display decoder ROMs
- CPU microcode ROMs
- Extended microcode with conditional flags

This project is based on the educational work of **Ben Eater** and serves as an excellent introduction to EEPROM programming, shift registers, and computer architecture.

---

# ✨ Features

- 🔹 Program 28C16 EEPROMs
- 🔹 Program 28C64 EEPROMs
- 🔹 Program 28C256 EEPROMs
- 🔹 Read EEPROM contents
- 🔹 Dump EEPROM memory
- 🔹 Verify programmed bytes
- 🔹 Generate ROM images
- 🔹 Program display decoder EEPROMs
- 🔹 Program CPU microcode EEPROMs
- 🔹 Supports conditional microcode
- 🔹 Uses inexpensive Arduino Nano
- 🔹 Uses only two 74HC595 shift registers
- 🔹 MIT Licensed

---

# 🎯 Project Objectives

The main goals of this project are:

- Learn how parallel EEPROM memories work.
- Understand address and data buses.
- Build a low-cost EEPROM programmer.
- Learn how shift registers expand Arduino I/O.
- Generate ROM images for digital logic projects.
- Build EEPROMs used inside an 8-bit computer.
- Explore low-level computer architecture.

---

# 🛠 Hardware Components

The programmer requires only a few inexpensive components.

| Component | Quantity |
|------------|---------:|
| Arduino Nano / Uno | 1 |
| 74HC595 Shift Register | 2 |
| 28C16 EEPROM | 1 |
| 28C64 EEPROM | Optional |
| 28C256 EEPROM | Optional |
| Breadboard | 1 |
| Jumper Wires | Several |
| USB Cable | 1 |
| 5V Power Supply | 1 |

---

# 💾 Supported EEPROM Chips

This programmer supports most parallel EEPROM devices in the **28C family**.

| EEPROM | Size |
|---------|------|
| AT28C16 | 2 KB |
| AT28C64 | 8 KB |
| AT28C256 | 32 KB |

Other compatible EEPROMs with the same interface can also be programmed after making small adjustments to the address width.

---

# 🧩 Why Use Shift Registers?

One of the biggest limitations of the Arduino Nano is the number of available digital pins.

Programming an EEPROM requires controlling:

- Address Lines
- Data Bus
- Output Enable
- Write Enable
- Chip Enable

This quickly exceeds the available GPIO pins.

To solve this problem, the project uses **two 74HC595 Serial-In Parallel-Out Shift Registers**.

Benefits include:

- ✅ Drastically fewer Arduino pins required
- ✅ Simple serial communication
- ✅ Easy scalability
- ✅ Faster addressing
- ✅ Clean wiring

Instead of directly driving every address line, the Arduino simply shifts the address bits into the two 74HC595 chips.

The shift registers then hold the address stable while the EEPROM is being programmed.

---

# 🔌 Circuit Diagram

The complete wiring diagram is included in this repository.

<p align="center">
    <img src="schematic.png" width="900">
</p>

The schematic illustrates:

- Arduino Nano connections
- EEPROM wiring
- Shift register connections
- Address bus
- Data bus
- Output Enable
- Write Enable
- Power connections

---

# ⚙️ How It Works

Programming an EEPROM follows a simple sequence:

1. Load the desired address into the shift registers.
2. Present the data byte on the data bus.
3. Enable the EEPROM.
4. Pulse the **Write Enable** pin.
5. Wait for the internal write cycle.
6. Repeat for the next memory address.

When reading:

1. Load the address.
2. Enable Output Enable.
3. Read the data bus.
4. Display or store the value.

# 📂 Repository Structure

```text
Arduino-EEPROM-Programmer/
│
├── eeprom-programmer.ino
├── multiplexed-display.ino
├── microcode-eeprom-programmer.ino
├── microcode-eeprom-with-flags.ino
├── schematic.png
└── README.md
```

Each sketch in this repository targets a different application while using the same EEPROM programmer hardware.

---

# 📄 Included Sketches

This repository contains four Arduino sketches.

Each one corresponds to a different stage of the project.

---

## 1️⃣ Basic EEPROM Programmer

**File**

```text
eeprom-programmer.ino
```

This is the recommended starting point.

It demonstrates the complete EEPROM programming process.

### Features

- Write bytes to EEPROM
- Read bytes back
- Dump EEPROM contents
- Verify written data
- Address manipulation
- Data bus control

This sketch teaches the fundamentals of EEPROM programming before moving to more advanced projects.

---

## 2️⃣ Multiplexed Display EEPROM

**File**

```text
multiplexed-display.ino
```

This sketch generates an EEPROM image used as a ROM lookup table for driving a multiplexed 4-digit seven-segment display.

Instead of using software calculations, the EEPROM instantly returns the correct segment pattern.

### Features

- Converts binary numbers
- Generates display lookup tables
- Drives seven-segment displays
- Extremely fast lookup

Applications include:

- Digital counters
- Clocks
- Breadboard computers
- Embedded displays

---

## 3️⃣ CPU Microcode EEPROM

**File**

```text
microcode-eeprom-programmer.ino
```

This sketch generates the microcode ROM used inside an 8-bit breadboard computer.

Instead of wiring complex combinational logic, the CPU simply reads the next control word directly from EEPROM.

### Generates

- Fetch cycle
- Execute cycle
- Control signals
- Instruction decoder

This dramatically simplifies CPU design.

---

## 4️⃣ Microcode with Flags

**File**

```text
microcode-eeprom-with-flags.ino
```

This version expands the previous microcode by adding support for CPU flags.

Supported flags include:

- Zero Flag
- Carry Flag

These flags allow conditional instructions such as:

- Jump if Zero
- Jump if Carry
- Branch instructions

This makes the CPU significantly more capable.

---

# 🚀 Getting Started

## Requirements

Before using this project ensure you have:

- Arduino IDE
- USB Cable
- Arduino Nano
- EEPROM
- Breadboard
- Shift Registers

---

# 🔨 Installation

### Clone the repository

```bash
git clone https://github.com/yourusername/Arduino-EEPROM-Programmer.git
```

### Open Arduino IDE

Load the desired sketch.

For beginners:

```text
eeprom-programmer.ino
```

is recommended.

---

# ▶ Upload the Sketch

1. Connect Arduino.
2. Select the correct COM port.
3. Select the board.
4. Upload.

After uploading the Arduino becomes an EEPROM programmer.

---

# 💻 Using the Programmer

Connect the EEPROM according to the schematic.

Run the sketch.

The Arduino will:

- Shift addresses into the 74HC595 registers.
- Place data onto the EEPROM bus.
- Toggle the Write Enable pin.
- Program the memory.
- Verify written bytes.

---

# 📊 Programming Sequence

Programming a single byte involves:

```text
Address
      ↓
Shift Registers
      ↓
EEPROM Address Bus
      ↓
Place Data
      ↓
Write Enable Pulse
      ↓
Internal EEPROM Write
      ↓
Verification
```

This sequence is repeated until all requested addresses have been programmed.

---

# 🧠 How Microcode Works

Instead of implementing CPU logic using hundreds of logic gates, this project stores control signals inside EEPROM.

Every instruction corresponds to one or more control words.

The CPU simply reads the EEPROM and activates the required control signals.

Benefits include:

- Easier debugging
- Easier expansion
- Cleaner CPU design
- New instructions can be added by reprogramming the EEPROM

---

# 🎮 Example Applications

The programmed EEPROMs can be used for:

- Breadboard CPUs
- Instruction decoders
- Seven-segment displays
- Digital clocks
- ROM lookup tables
- Binary decoders
- Embedded projects
This process is repeated until the entire EEPROM has been programmed or dumped.

---
---

# 📈 Performance

The programmer is designed to provide reliable EEPROM programming while keeping the hardware simple and inexpensive.

### Advantages

- Reliable EEPROM programming
- Low hardware cost
- Minimal component count
- Easy to understand
- Easy to modify
- Suitable for beginners
- Excellent learning platform

---

# 🔍 Troubleshooting

## Arduino Cannot Detect EEPROM

Possible causes:

- Incorrect wiring
- Missing power connection
- Wrong EEPROM orientation
- Loose jumper wires

### Solution

- Verify every connection using the schematic.
- Check that the EEPROM notch orientation is correct.
- Measure the 5V supply.
- Ensure all GND connections are shared.

---

## Programming Fails

Possible causes:

- Incorrect Write Enable timing
- EEPROM write protection
- Faulty EEPROM

### Solution

- Verify the WE pulse timing.
- Test another EEPROM.
- Read the EEPROM before programming to ensure communication is working.

---

## Incorrect Data Read Back

Possible causes:

- Address bus errors
- Shift register wiring
- Floating data lines

### Solution

- Check the 74HC595 wiring.
- Verify the latch and clock pins.
- Confirm that all address lines are connected correctly.

---

## Shift Registers Not Working

Check:

- Data pin
- Clock pin
- Latch pin
- Power
- Ground

A single loose wire can prevent the address from being loaded correctly.

---

# ❓ Frequently Asked Questions

### Why are two 74HC595 chips used?

The Arduino Nano does not have enough digital pins to directly drive every EEPROM address line.

Two 74HC595 shift registers allow many address lines to be controlled using only a few Arduino pins.

---

### Why use EEPROM instead of Flash?

Parallel EEPROMs:

- can be reprogrammed easily,
- are ideal for breadboard computers,
- allow fast experimentation.

---

### Can I use an Arduino Uno?

Yes.

The sketches are compatible with both Arduino Uno and Arduino Nano.

---

### Which EEPROM chips are supported?

The programmer supports:

- AT28C16
- AT28C64
- AT28C256

and many compatible EEPROM devices.

---

# 📚 References

This project was inspired by the educational work of **Ben Eater**.

Recommended resources:

- Ben Eater's 8-Bit Computer Series
- Arduino Documentation
- AT28C16 Datasheet
- AT28C64 Datasheet
- AT28C256 Datasheet
- 74HC595 Datasheet

These resources provide an excellent understanding of EEPROM programming and digital computer architecture.

---

# 🎥 Recommended Video Series

If you want to understand how every sketch in this repository works, the following videos are highly recommended:

### Build an Arduino EEPROM Programmer

Introduces the hardware and demonstrates how the programmer works.

---

### Build an 8-bit Decimal Display

Shows how EEPROM can replace combinational logic for driving seven-segment displays.

---

### Reprogramming CPU Microcode

Explains how EEPROM stores CPU control signals.

---

### Adding Machine Language Instructions

Demonstrates extending the CPU instruction set by updating the microcode.

---

### Conditional Jump Instructions

Introduces CPU flags and conditional branching using EEPROM-based microcode.

---

# 🎓 Educational Objectives

After completing this project, you should understand:

- EEPROM architecture
- Parallel memory devices
- Shift registers
- Address buses
- Data buses
- Read/Write timing
- Arduino GPIO control
- Digital logic
- ROM lookup tables
- CPU microcode
- Instruction decoding
- Computer architecture fundamentals

---

# 🤝 Contributing

Contributions are welcome.

Possible improvements include:

- Supporting additional EEPROM families
- Performance optimizations
- Better memory verification
- PCB design
- Graphical interface
- Serial command interface
- Automatic chip detection

Feel free to fork the repository and submit a pull request.

---

# 📜 License

This project is released under the **MIT License**.

The original hardware concept and educational material were created by **Ben Eater**.

This repository is intended for educational purposes and further experimentation.

---

# 🙏 Acknowledgements

Special thanks to:

- **Ben Eater** for his outstanding educational content.
- The Arduino community.
- Open-source hardware contributors.
- Everyone who shares knowledge about digital electronics and computer architecture.

---

# ⭐ Support

If you found this project useful:

- ⭐ Star the repository
- 🍴 Fork the project
- 🛠️ Improve the code
- 📝 Open an issue
- 🚀 Share it with others

Your support helps improve educational open-source projects.

---

<p align="center">

**Made with ❤️ using Arduino, C++, EEPROM, and Digital Logic**

</p>
