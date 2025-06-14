# 📡 Mobile Radio FoxBot (Senior Capstone Project)

**Duration:** Aug 2024 – May 2025  
**Team Size:** 4  
**Role:** Lead Power Board Designer & Embedded Developer  
**Tools Used:** C++, FreeRTOS, Altium Designer, I2C, ESP32, Embedded Systems

---

## 🚀 Overview

The Mobile Radio FoxBot is a battery-powered autonomous system designed for high-frequency signal tracking and mobile communication in a field environment. Amateur Radio Directional Finding (ADRF) is a sport in which an individual tries to locate a hidden transmitting device. Our goal was to develop a rover that will complete this task. Additionally, our robot will increase the potential of ARDF training and aid in the engineering of directional antennas. 


## 🛠️ Key Contributions

- **Designed a custom 4-layer power PCB** with 3 isolated power rails (3.3V, 5V, 7.4V) and 3 independent battery monitoring circuits.
- **Implemented I2C-based battery monitoring** for accurate state-of-charge reporting, reducing data error rates by 30%.
- **Used FreeRTOS with C++** to acquire and process real-time sensor data, improving system response and telemetry reliability.
- **Collaborated with a cross-functional team** to develop an autopilot system using GPS and walkie-talkie integration for remote operation.
- Conducted hardware testing and validation using oscilloscopes, logic analyzers, and custom debug firmware.

---

## 📸 Images and Schematics
| 3.3V Converter| 5.3V Converter|
|---------------|---------------|
| ![11.1V to 3.3V Converter](./Images/3.3V_Schematic.png)|![11.1V to 5.3V Converter](./Images/5.3V_Schematic.png)|


---

| 7.4V Converter| Push to Talk Circuit |
|---------------|---------------|
![11.1V to 7.4V Converter](./Images/7.4V_Schematic.png)|![Push to Talk Circuit](./Images/PTT_Schematic.png)|

---

These convters each designed for specific components on the Mobile Radio FoxBot. Each of these are connected to a 3 cell Lipo battery, which operates at 11.1 V. First, the 3.3V converter for powering the ESP32. The 5.3V converter is for powering the Pixhawk, DTMF decoder, and the ultrasonic sensors. The 7.4V converter was constructed to power the Baofeng radio. The push to talk schematic was used so that the ESP32 could control when the push to talk is on or off on the Baofeng Radio, this was important for establishing communication between user and rover. This was done using the ground of the speaker and microphone and connecting them via a transistor. Then have the speaker connected to a DAC pin on the ESP32.

---

### 🔋 Battery Monitior
|Battery Monitior |
|---------------|
![Battery Monitior](./Images/Battery_Monitor_Schematic.png)|

---
The rover was built using 3 seperate 3 cell lipo batteries. Thus there was a need for three seperate battery monitoring system for each of the batteries that will comunicate to ESP32 and have battery charge, and discharge rate avaliable.

---

## 📘 Integrated Schematics

| File | Description |
|------|-------------|
| [`IntegratedSchematic_v1.SchDoc`](./Altium_Files/IntegratedSchematic_v1.SchDoc) | Altium Designer Integrated Schematic File |

---
This file contains all the shcematics that are required for the rover, this has all the integrated schematics.

## PCB Design
| Image|
|---------------|
![PCB](./Images/PCB.png)|
|---------------|
![PCB](./Images/ESP32_Pinout.png)|

| File | Description |
|------|-------------|
| [`PCB1.PcbDoc`](./Altium_Files/PCB1.PcbDoc) | Altium Designer Integrated PCB File |
| [`Schematic_Library.SchLib`](./Altium_Files/Schematic_Library.SchLib) | Altium Designer Schematic Library |
| [`PCB_Library.PcbLib`](./Altium_Files/PCB_Library.PcbLib) | Altium Designer PCB Library |
| [`CapStone_BOM.xlsx`](./Altium_Files/CapStone_BOM.xlsx) | Bill of Materials for PCB |

---

## 📸 ESP32 Programming
The ESP32 played an essintial part in the Mobile Radio Foxbot. I began by setting up the general flow that the program will follow. Because our communication is via Baofeng radio I established the Push to Talk control as seen in the [PTT Schemaitc](#-Images-and-Schematics). Then, having the DTMF decoder outputing bits in binary to the pins of the ESP32 this would allow the ESP to understand the signal being sent to the Foxbot. 
