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


loop()
{
    read_temperature();
    read_interrupts();
    receive_fuel_data();
    update_LCD();
    send_indicator_status();
}

### 🔄 CAN Communication
[FUEL NODE] -----> (Fuel %) -----> [MAIN NODE]
[MAIN NODE] -----> (Indicator Signals) -----> [INDICATOR NODE]


- CAN frames enable communication between nodes  
- Main node acts as **coordinator**  
- Continuous real-time data exchange  

---
## 🌡️ Sensor Processing

### 🔹 Temperature (DS18B20)
- Digital sensor (1-Wire protocol)  
- Periodic sampling  
- Displayed on LCD  

### 🔹 Fuel Level (ADC)
- Analog input via fuel gauge  
- Converted to percentage  
- Sent via CAN  

---

## 🚨 Indicator Control Logic

- Triggered using **external interrupts (EINT0 / EINT1)**  
- Main node processes event  
- Sends CAN message  
- Indicator node activates LEDs  


Interrupt → Main Node → CAN → Indicator Node → LED


---

## 📺 LCD Display System

Displays real-time vehicle parameters:


Temp: 85°C
Fuel: 60%
Indicator: ON


---

## 🧩 Node Architecture

### 🔹 Main Node
- Reads temperature  
- Receives fuel data  
- Handles interrupts  
- Updates LCD  
- Sends indicator signals  

### 🔹 Fuel Node
- Reads fuel using ADC  
- Sends data via CAN  

### 🔹 Indicator Node
- Receives CAN messages  
- Controls LEDs  

---

## 🚀 Getting Started

### 🛠️ Requirements
- Keil uVision  
- Flash Magic  
- LPC2129 Development Board  
- Embedded C Knowledge  

### ▶️ Steps
```bash
git clone https://github.com/your-username/drivewatch.git
Open project in Keil
Compile code
Flash using Flash Magic
Observe output on LCD
🛠️ Implementation Steps
Test LCD display
Test ADC with variable voltage
Implement fuel reading
Implement temperature sensor
Test interrupts
Test CAN communication
Integrate all modules
