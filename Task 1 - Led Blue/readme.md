# 💡 VSDSquadron FPGA Mini – Blue LED Project

## 📘 Task 1 Overview
This project demonstrates how to glow the **blue LED** on the **RGB LED** of the **VSDSquadron FPGA Mini (FM)** board using **Verilog HDL**.  
It includes understanding the Verilog code, creating the **PCF (Physical Constraint File)**, integrating it with the FPGA Mini board, and successfully programming the FPGA using open-source tools.

---

## 🧩 Step 1: Understanding the Verilog Code
**Verilog Source:** [`top.v`](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%201%20-%20Led%20Blue/top.v)

### 🔍 Module Overview
| Signal | Direction | Description |
|:--------|:-----------|:-------------|
| `led_red`, `led_blue`, `led_green` | Output | Control RGB LED colors |
| `hw_clk` | Input | Hardware oscillator clock input |
| `testwire` | Output | Test signal connected to frequency counter bit 5 |

### 🧠 Internal Component Analysis
#### 1. Internal Oscillator (`SB_HFOSC`)
Generates the internal clock signal used by the frequency counter.  
**Control Signals:**
- `CLKHFPU = 1'b1` → Power up oscillator  
- `CLKHFEN = 1'b1` → Enable oscillator  
- Output: `CLKHF` → Connected to internal logic  

#### 2. Frequency Counter
- Implemented as a **27-bit register** (`reg [26:0] counter`).  
- Increments on every positive edge of the internal oscillator (`int_osc`).  
- **Bit 5** is routed to `testwire` for monitoring.

#### 3. RGB LED Driver (`SB_RGBA_DRV`)
Manages the RGB LED brightness and color output.  
- Enables LED operation: `RGBLEDEN = 1'b1`
- Sets brightness:
  - `RGB0PWM = 1'b0` → Red LED off  
  - `RGB1PWM = 1'b0` → Green LED off  
  - `RGB2PWM = 1'b1` → Blue LED on (maximum brightness)  
- Current settings: `CURREN = 0b000001` for equal current distribution.

### 🎯 Purpose of the Code
This Verilog module drives the **blue LED** of the onboard RGB LED at full brightness using an internal oscillator and counter logic.  
It demonstrates basic control of FPGA I/O and internal clock usage.

---

## 📄 Step 2: Creating the PCF File
**PCF Source:** [`VSDSquadronFM.pcf`](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%201%20-%20Led%20Blue/VSDSquadronFM.pcf)

### 🔌 Pin Assignments
| Signal | Pin | Description |
|:--------|:----|:-------------|
| `led_red` | 39 | Controls red LED pin |
| `led_blue` | 40 | Controls blue LED pin |
| `led_green` | 41 | Controls green LED pin |
| `hw_clk` | 20 | Hardware clock input |
| `testwire` | 17 | Test signal output |

Each mapping ensures correct connection between the logical Verilog signals and the physical FPGA board pins.

---

## ⚙️ Step 3: Integration with VSDSquadron FPGA Mini Board
Refer to the **VSDSquadron FPGA Mini board datasheet** for details on features, pinout, and programming procedures.

### 🧭 Setup Steps
1. **Connect** the FPGA Mini board to your computer via USB-C.  
   - Check connection with:  
     ```bash
     lsusb
     ```
     Look for *“Future Technology Devices International”* to confirm FTDI detection.

2. **Prepare Files:**
   - `top.v`
   - `VSDSquadronFM.pcf`
   - `Makefile` ([Link](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%201%20-%20Led%20Blue/Makefile))

3. **Build & Flash Commands:**
   ```bash
   make clean       # Clear old builds
   make build       # Compile the design
   sudo make flash  # Program the FPGA

