# ⚙️ VSDSquadron FPGA Mini (FM) Board

### 🏷️ Developed by [VLSI System Design (VSD)](https://www.vlsisystemdesign.com/)

![Alt text](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/vsd%20image.jpg)


The **VSDSquadron FPGA Mini (FM)** board is a **compact, low-cost FPGA prototyping platform** that integrates an onboard programmer, SPI flash, RGB LED, and easily accessible GPIO pins — enabling rapid FPGA design and experimentation.

---
![Alt text](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/VSDSquadron%20FPGA%20Mini%20Front.jpg)


## 🧠 Overview

The VSDSquadron FM board provides a hands-on, open-source environment for learning and implementing FPGA-based designs.  
It is powered by the **Lattice UltraPlus ICE40UP5K FPGA**, known for low power, flexible I/O, and high-density logic cells.

### 🔹 Key Features

- **FPGA:** Lattice iCE40UP5K-SG48ITR  
  - 5.3K LUTs, 1Mb SPRAM, 120Kb DPRAM  
  - 8 multipliers for DSP applications  
- **Connectivity:** FTDI FT232H USB-to-SPI for communication and programming  
- **GPIO:** 32 accessible FPGA I/O pins for easy prototyping  
- **Memory:** 4 MB SPI Flash for configuration and data storage  
- **LEDs:** Onboard RGB LED for status indication or custom logic output  
- **Form Factor:** 57 mm × 29 mm board size, lightweight and portable  
- **Power:** Integrated 3.3 V / 1.2 V regulators with external 3.3 V supply option  

---

## 📦 Kit Contents

| Item | Quantity | Description |
|:------|:-----------:|:------------|
| VSDSquadron FPGA Mini (FM) board | 1 | Board with ICE40UP5K FPGA, RGB LED, SPI Flash, and onboard power regulation |

---

## 📊 Technical Specifications

| Feature | Specification |
|:--------|:---------------|
| Technology Node | 40 nm |
| Logic Cells | 5,280 |
| Flip-Flops | 4,960 |
| SRAM Blocks | 120 Kb |
| I/O Pins | 39 |
| Core Voltage | 1.2 V |
| I/O Voltage | 3.3 V / 2.5 V / 1.8 V |
| Max Frequency | 133 MHz |
| Operating Temp | 20 °C – 35 °C (Room temperature) |
| Tools Supported | Yosys · NextPNR · Project IceStorm |

---

## 💻 Software Installation (Windows)

To run and program FPGA projects, the datasheet recommends setting up a **Linux virtual environment** via **Oracle VirtualBox**.

### Installation Summary
1. Ensure at least **100 GB free disk space**.
2. **Download the VSDSquadron FPGA Mini Software Bundle**  
   [vsdsquadron_fpga_mini.zip](https://vsd-labs.sgp1.cdn.digitaloceanspaces.com/vsd-labs/vsdsquadron_fpga_mini.zip)
3. Install **Oracle VirtualBox** from [virtualbox.org](https://www.virtualbox.org/wiki/Downloads)
4. Create a new virtual machine:
   - OS Type: Linux  |  Version: Xubuntu 64-bit  
   - RAM: 4 GB  |  CPU Cores: 4
5. Use the provided **VDI file** as the existing virtual hard disk.
6. Log in with password `vsdiat`.

---
## 🙏 Acknowledgment

A heartfelt thank-you to **[Kunal Ghosh](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/)** — founder of **VLSI System Design (VSD)** — for his leadership in promoting open-source hardware education.  

His efforts in building the **VSDSquadron ecosystem** and making **FPGA learning accessible** continue to empower students, educators, and engineers worldwide.  

**Thank you, Kunal,** for inspiring a new generation of open-source silicon designers.


