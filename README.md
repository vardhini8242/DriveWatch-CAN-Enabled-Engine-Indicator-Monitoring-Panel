# 🚗 DriveWatch: CAN-Enabled Engine & Indicator Monitoring Panel



Real-time vehicle monitoring system built using **CAN protocol**, capable of decoding engine parameters and displaying them on an LCD dashboard — fully embedded, no cloud dependency.

---

## 📑 Table of Contents
- [Overview](#-overview)
- [Hardware](#-hardware)
- [Architecture](#-firmware-architecture)
- [CAN Communication](#-can-communication-flow)
- [Sensor Processing](#-sensor-processing)
- [Indicator Logic](#-indicator-control-logic)
- [LCD Display](#-lcd-display-system)
- [Node Architecture](#-node-architecture)
- [Getting Started](#-getting-started)
- [Implementation](#-implementation-steps)
- [Debugging](#-debugging-notes)
- [Project Structure](#-project-structure)
- [Future Scope](#-future-roadmap)

---

## 🔍 Overview

DriveWatch is an embedded automotive monitoring system designed to interface directly with a vehicle’s **CAN (Controller Area Network) bus**.

It decodes real-time vehicle data such as:
- 🌡️ Engine temperature  
- ⛽ Fuel level  
- 🚨 Warning indicators  

and displays them on an LCD dashboard for the driver.

### ✨ Key Features
- CAN-based real-time communication  
- Multi-node embedded architecture  
- LCD dashboard display  
- DS18B20 temperature sensing  
- ADC-based fuel monitoring  
- Interrupt-driven indicator alerts  
- Fully standalone system (no OS, no cloud)

---

## ⚙️ Hardware

| Component | Description |
|----------|------------|
| LPC2129 | Main microcontroller |
| MCP2551 | CAN transceiver |
| LCD | Display output |
| DS18B20 | Temperature sensor |
| Fuel Gauge | Analog input |
| LEDs | Indicator output |
| Switches | Interrupt triggers |
| USB-UART | Programming interface |

---

## 🧠 Firmware Architecture

The system follows a **modular multi-node architecture**.

### Main Loop (Main Node)

```c
loop()
{
    read_temperature();
    read_interrupts();
    receive_fuel_data();
    update_LCD();
    send_indicator_status();
}
