# 🔧 BLDC Motor Control Using Minimal Hall Sensors

## 📘 Project Overview

This project, developed as part of ECEN 441 (Digital Control Systems) at Texas A&M University, focuses on the **design and implementation of a two-phase Brushless DC (BLDC) motor control system**. The objective was to reduce the number of required Hall sensors and magnets—without compromising precise rotor position detection or torque generation.

The final design successfully uses **only two Hall effect sensors** and **two permanent magnets** (each spanning 180°) to produce four distinct energizing states (A+, B+, A−, B−) for accurate rotor commutation and consistent torque output.

---

## 🎯 Project Goals

- Replace the traditional 4-sensor model with a **2-Hall sensor system**
- Design a logic system to derive **4 output states from 2-bit input**
- Achieve **constant clockwise torque** during motor rotation
- Minimize power electronics complexity
- Provide a scalable control strategy for low-cost BLDC applications

---

## 🌀 System Design

### 📐 Coil and Magnet Arrangement

- Rotor includes two magnets (North & South), each covering 180°.
- Stator includes four coils placed at:
  - 0°: A+
  - 90°: B+
  - 180°: A−
  - 270°: B−
- Two Hall sensors placed at **225° and 315°**, ensuring four unique digital outputs per revolution: `(00), (01), (10), (11)`.

### 🔄 Commutation Logic

The Hall sensor outputs feed into digital logic circuitry that controls MOSFET switches for coil energizing.

| Step | Rotor Position (°) | Active Switches | Energized Coil |
|------|--------------------|-----------------|----------------|
| 1    | 315–45             | S5 & S6         | B+             |
| 2    | 45–135             | S3 & S4         | A−             |
| 3    | 135–225            | S7 & S8         | B−             |
| 4    | 225–315            | S1 & S2         | A+             |

### 💡 Truth Table Logic

| Coil   | Step 1 | Step 2 | Step 3 | Step 4 |
|--------|--------|--------|--------|--------|
| A+     | 0      | 0      | 0      | 1      |
| B+     | 1      | 0      | 0      | 0      |
| A−     | 0      | 1      | 0      | 0      |
| B−     | 0      | 0      | 1      | 0      |

| Hall Sensor | Step 1 | Step 2 | Step 3 | Step 4 |
|-------------|--------|--------|--------|--------|
| H1          | 1      | 0      | 0      | 1      |
| H2          | 0      | 0      | 1      | 1      |

---

## 🔌 Power Electronics

Two full H-bridges (one per coil: A and B) enable bidirectional current flow:

- **A coil** uses S1–S4
- **B coil** uses S5–S8

This setup enables precise polarity control for A+/A− and B+/B− excitation states, ensuring torque continuity.

Each H-bridge activates a pair of switches per state based on Hall input.

---

## 🧠 Digital Logic and Signal Processing

The logic circuit interprets Hall sensor inputs to determine coil activation. The transitions between coil states are timed such that **the next phase activates halfway (45°) into the current phase**, maintaining smooth torque and avoiding dead zones.

Figures (in report):
- **Figure 6:** Hall sensor timing diagram
- **Figure 8:** Final logic circuit
- **Table 2:** Truth table for logic design

---

## 🧭 System Block Diagram

```
[BLDC Motor] → [Hall Sensors] → [Digital Logic] → [MOSFET Switching] → [Coils] → Loop
```

Each block functions cyclically to maintain continuous feedback and motion.

---

## ✅ Results and Conclusion

- Achieved **constant torque** during full motor revolution using only **2 Hall sensors**.
- Produced **four clean switching states** required for two-phase BLDC operation.
- Logic minimized complexity while maximizing reliability.
- Full system successfully simulated and validated.

This project demonstrates an optimized approach to BLDC motor control, reducing sensor and hardware complexity while maintaining accurate, robust operation. It’s particularly well-suited for embedded, robotics, or low-cost automation systems.

---

## 📎 Project Assets

- Full report: [`ECEN_441_Term_Project_Report.pdf`](./ECEN 441 Term Project Report.pdf)
- Timing Diagrams and Logic Tables
- H-Bridge Circuit Schematics
- Truth Tables for Control Logic

