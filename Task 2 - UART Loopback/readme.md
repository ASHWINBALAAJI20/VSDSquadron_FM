# 📡 Task 2 : UART Loopback

**Objective:** Implement a **UART loopback mechanism** where transmitted data is immediately received back, facilitating comprehensive testing and verification of the UART's core functionality.

---

## 🧐 What is a UART?

A **UART (Universal Asynchronous Receiver/Transmitter)** is a serial communication protocol common in embedded systems. It uses dedicated **TX** (Transmit) and **RX** (Receive) lines and operates **asynchronously**, meaning it requires no shared clock. Successful communication relies on both the transmitter and receiver using the same **Baud rate** (e.g., 9600).

---

## 💻 Step 1: Analyzing the Existing Verilog Code

The implementation is based on two Verilog files: `top.v` and `uart_trx.v`.

### 1. `top.v` Analysis (Top-Level Module)

This module handles physical I/O and the core loopback mechanism.

| Port Name | I/O | Description |
| :--- | :--- | :--- |
| `led_red`, `led_blue`, `led_green` | Output | Control pins for the on-board RGB LED. |
| `uarttx` | Output | UART Transmission pin. |
| `uartrx` | Input | UART Receiver pin. |

#### Internal Components & Loopback Logic:

* **Internal Oscillator (`SB_HFOSC`):** Generates the internal clock signal (`int_osc`) required for system operation. Configuration: `CLKHFPU = 1'b1`, `CLKHFEN = 1'b1`.
* **Frequency Counter:** A **27-bit register** that increments with every clock cycle, used for timing and general testing (`frequency_counter[5]` is routed to a test wire).
* **RGB LED Driver:** Configured to set **Red** (`RGB0PWM = 1'b0`) and **Green** (`RGB1PWM = 1'b0`) to minimum brightness, and **Blue** (`RGB2PWM = 1'b1`) to maximum brightness.
* **Core Loopback:** The key implementation is the direct wire assignment:
    ```verilog
    assign uarttx = uartrx;
    ```
    This instantly echoes any data received on `uartrx` back out on `uarttx`, fulfilling the loopback objective.

### 2. `uart_trx.v` Analysis (UART TX 8N1 Transmitter)

This module defines the state machine for standard 8-bit, No parity, 1-stop bit (8N1) transmission.

| Port Name | I/O | Description |
| :--- | :--- | :--- |
| `clk` | Input | System clock. |
| `txbyte` | Input | 8-bit data to be transmitted. |
| `senddata` | Input | Trigger to start transmission. |
| `txdone` | Output | Indicates transmission completion. |
| `tx` | Output | UART transmission line. |

#### State Machine Parameters:

| State Name | Value | Description |
| :--- | :--- | :--- |
| `STATE_IDLE` | 2'b00 | Waits for the `senddata` trigger. |
| `STATE_STARTTX` | 2'b01 | Sends the **Start bit (0)**. |
| `STATE_TXING` | 2'b10 | Sends the **8-bit data** (LSB first). |
| `STATE_TXDONE` | 2'b11 | Sends the **Stop bit (1)**, then returns to IDLE and asserts `txdone`. |

---

## 📐 Step 2: Design Documentation

### Block Diagram for UART Loopback

This diagram illustrates the logical path of the loopback data.



[Image of UART Loopback block diagram]


### Detailed Circuit Diagram

This diagram shows the connection between the internal FPGA module and the external peripherals/pins.



---

## 🛠️ Step 3: Implementation on the FM Board

To implement the code on the **VSDSquadron FPGA Mini**, ensure the project folder contains `top.v`, `uart_trx.v`, the appropriate **PCF** (Pin Constraint File), and a **Makefile**.

1.  **Check Connection:** Open the Ubuntu terminal and confirm the device is connected.
    ```bash
    lsusb
    ```
2.  **Navigate:** Change directory to the `uart_loopback` project folder.
    ```bash
    cd <folder name>
    ```
3.  **Build:** Execute the make command to synthesize the code and build the binaries (bitstream).
    ```bash
    make build
    ```
4.  **Flash:** Use the make command with `sudo` to program the board.
    ```bash
    sudo make flash
    ```
The code is now implemented on the FM board.

---

## ✅ Step 4: Testing and Verification

Verification is performed using a serial terminal application like **Docklight**.

1.  **Configure Terminal:** Open the serial terminal and set the communication parameters:
    * **Baud rate:** Set to **9600**.
    * **COM Port:** Select the port connected to the FPGA Mini's USB interface.
2.  **Send Data:** Enter the desired test command/sequence in the send box (e.g., in Docklight's "Send Sequences").
3.  **Execute:** Trigger the sequence transmission.

### Verification Result

The terminal should immediately display the **exact same data** in the receive window that was just transmitted. This confirms the successful operation of the loopback mechanism: data transmitted from the PC reaches the FPGA's `uartrx` pin and is instantly echoed back out on the `uarttx` pin.



---

## 📹 Step 5: Final Documentation

A short video demonstrating the UART loopback functionality, showing the transmission of a sequence and the immediate receipt of the same sequence in the serial terminal, will be recorded to complete the documentation.
