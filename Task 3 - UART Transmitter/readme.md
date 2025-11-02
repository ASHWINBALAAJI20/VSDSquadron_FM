# 💡 VSDSquadron FPGA Mini – UART Transmitter Project

## 📘 Task 3 Overview
This project demonstrates how to establish **UART communication** between the **VSDSquadron FPGA Mini (FM)** board and a PC using **Verilog HDL**.  
The FPGA continuously transmits the character `'D'` over UART to the connected PC terminal.  
This example focuses **only on data transmission**, not reception, making it an ideal demonstration of a **UART transmitter** design.

---

## 🧩 Step 1: Studying the Existing Code
**Verilog Sources:**
- [`top.v`](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/top.v)
- [`uart_trx.v`](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/uart_trx.v)

> The file `uart_trx.v` contains the UART transmission logic (8 data bits, no parity, 1 stop bit — 8N1 format).  
> Since it is similar to the one discussed in **Task 2**, this analysis focuses mainly on the **`top.v`** module.

---

### 🔍 Analysis of `top.v`

#### Module Description
The `top.v` module defines five ports — four outputs and one input:

| Signal | Direction | Description |
|:--------|:-----------|:-------------|
| `led_red`, `led_green`, `led_blue` | Output | Drive the RGB LED on the FPGA board |
| `uarttx` | Output | UART transmit output pin |
| `hw_clk` | Input | Hardware oscillator clock input |

---

#### UART Transmitter Instantiation

The UART transmitter (`uart_tx_8n1`) is instantiated as follows:

uart_tx_8n1 DanUART (
    .clk(clk_9600),
    .txbyte("D"),
    .senddata(frequency_counter_i[24]),
    .tx(uarttx)
);
---
## 🧠 Working Principle

The internal counter in the **top module** periodically triggers the UART transmission of the character **'D'**.

The **UART transmitter module** formats the data according to the **8N1 standard**:
- **8 data bits**  
- **No parity**  
- **1 stop bit**

The FPGA sends `'D'` repeatedly over the **UART TX line** at a **9600 baud rate**.  
The **RGB LEDs** are used for visual debugging and indication, controlled by counter signals within the module.

---

## 📄 Step 2: Block Diagram

### 🧱 Block Diagram
The block diagram shows the internal structure of the **UART Transmitter system**.

![](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/Block%20Diagram.png)

---

### ⚡ Circuit Diagram
The circuit diagram below shows how the **UART TX pin** of the FPGA is connected to a **PC’s RX pin** through a **USB-to-UART converter (FTDI)**.

![](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/circuit%20diagram.png)

---

## 💻 Step 3: Implementation on the Board

Ensure the following essential files are present inside your **`Task 3`** folder, located within the **`VSDSquadron_FM`** project directory:

* `top.v`
* `uart_tx_8n1.v`
* `Makefile`
* `VSDSquadronFM.pcf`

### 🧭 Setup Steps

1.  **Connect** the FPGA Mini board to your PC using a **USB-C cable**.

2.  **Verify the connection** in your terminal:

    ```bash
    lsusb
    ```
    > 💡 **Look for "Future Technology Devices International"** in the output to confirm the board is detected.

3.  **Navigate** to the project folder:

    ```bash
    cd <folder_name>
    ```

4.  **Build** the project:

    ```bash
    make build
    ```

5.  **Program** the FPGA:

    ```bash
    sudo make flash
    ```

✅ **Once complete, the UART transmitter module is successfully programmed onto the FPGA Mini board.**

---

[![Video of the UART Transmitter terminal demonstration in terminal.webm](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/terminal.mp4)

## 🧪 Step 4: Testing and Verification

You can use a serial terminal program like **PuTTY** (Windows) or **picocom** (Linux) to view the UART output. You should observe a continuous stream of the character **'D'**.

### 🪟 Using PuTTY (Windows)

1.  Download and install **PuTTY**.
2.  Open **Device Manager** and check the **COM port number** assigned to the FPGA (it will usually be a USB Serial Port).
3.  Launch **PuTTY** and configure the session settings:

    * **Connection type:** Serial
    * **COM Port:** (As shown in Device Manager, e.g., `COM3`)
    * **Baud rate:** `9600`
    * **Data bits:** `8`
    * **Parity:** `None`
    * **Stop bits:** `1`
    * **Flow control:** `None`

4.  Click **Open**.

You should immediately see the continuous stream of the character **'D'**.

[![Video of the UART Transmitter putty demonstration in putty.webm](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/putty.webm)

### 🐧 Using Picocom (Ubuntu/Linux)

1.  Install **picocom**:

    ```bash
    sudo apt install picocom
    ```

2.  Run the serial terminal directly:

    ```bash
    sudo picocom -b 9600 /dev/ttyUSB0 --echo
    ```

    **Alternatively,** if your `Makefile` is configured for it, use the simplified command:

    ```bash
    sudo make terminal
    ```
    This command will automatically open the serial terminal and display the stream of **'D'** characters.


--

[![Video of the UART Transmitter board in Board.webm](https://github.com/ASHWINBALAAJI20/VSDSquadron_FM/blob/main/Task%203%20-%20UART%20Transmitter/Board.webm)


