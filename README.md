# 🔌 Arduino EEPROM Programmer

An Arduino Nano based EEPROM programmer for **28C16**, **28C64**, **28C256**, and compatible parallel EEPROMs.

This project uses two **74HC595 shift registers** to expand the Arduino's I/O and includes sketches for programming EEPROMs used in an 8-bit breadboard computer.

## ✨ Features

- Supports 28C16 / 28C64 / 28C256 EEPROMs
- Read, write and dump EEPROM contents
- Shift-register based address expansion
- 7-segment display ROM generator
- 8-bit computer microcode generator
- Conditional microcode (flags support)

## 📂 Included Files

- eeprom-programmer.ino
- multiplexed-display.ino
- microcode-eeprom-programmer.ino
- microcode-eeprom-with-flags.ino
- schematic.png

## 🛠 Hardware

- Arduino Nano
- 2× 74HC595
- 28C EEPROM
- Breadboard
- Jumper wires

## 🔧 Circuit

The repository includes a complete wiring schematic (`schematic.png`).

## 🎯 Applications

- EEPROM Programming
- ROM Generation
- Ben Eater 8-bit Computer
- Microcode Programming

## 📄 License

MIT License.

Originally inspired by Ben Eater's educational project.
