

# 🧮 Complex Division Calculator – Dual PIC16F877A System

This project implements a **floating-point division calculator** using **two PIC16F877A microcontrollers** programmed in assembly under MPLAB IDE. It uses a **16×2 LCD** and a **push button interface** for digit entry and results navigation. The system supports interactive digit-by-digit number input and offloads division computation to a co-processor for efficiency.

---

> 🏫 **Birzeit University – Faculty of Engineering & Technology**
> 📖 **ENCS4330 – Real-Time Applications & Embedded Systems**
> 📅 2nd Semester 2024/2025
> 👨‍🏫 Instructor: Dr. Hanna Bullata
> 📅 Due Date: June 22, 2025

---

## 🛠️ System Overview

### 🎛 Hardware Components

* **Master CPU (PIC16F877A)**:

  * Connected to:

    * 16×2 Character LCD (via PortD, 4-bit mode)
    * Push Button P (PortB.0 with pull-up resistor)
    * Co-processor via PortC (data transfer)
* **Co-Processor (PIC16F877A)**:

  * Performs division computation
  * Communicates back result to Master
* **External Components**:

  * 4 MHz Oscillator (with 2×15pF capacitors)
  * 10kΩ Pull-up resistor on MCLR pin
  * 4.7kΩ pull-up resistor on LCD RS pin
  * Optional internal pull-up for push button

---

## 🔄 System Behavior

1. **Startup**

   * LCD displays:

     ```
     Welcome to
     Division
     ```
   * Blinks 3 times (0.5s delay), then pauses 2s.

2. **Input First Number**

   * LCD: `Number 1` on line 1, cursor on line 2.
   * Push button:

     * Each click increments digit (0–9).
     * 10th click wraps back to 0.
   * No click for 1s → digit fixed.
   * Double-click → skip to decimal part.

3. **Input Decimal Part**

   * Same procedure as integer part.
   * First digit fixed → remaining digits replicated.

4. **Input Second Number**

   * Same flow as First Number.
   * LCD displays `Number 2` for 1s.

5. **Computation**

   * LCD shows `=` on line 1.
   * Master sends numbers to co-processor:

     * Sends size first → awaits acknowledgment
     * Sends digits byte by byte using interrupts
   * Co-processor divides numbers and sends result back.
   * Master displays:

     ```
     Result
     <division_result>
     ```

6. **Result Navigation**

   * Click → Toggle display between Number 1 and Number 2.
   * Double-click → Restart division process.

---

## 📂 Project Structure

| Folder/File                | Description                                    |
| -------------------------- | ---------------------------------------------- |
| `Master_CPU/`              | MPLAB project for Master microcontroller       |
| `CoProcessor/`             | MPLAB project for Co-Processor microcontroller |
| `proteus_schematic.pdsprj` | Proteus schematic with all components          |
| `README.md`                | This documentation                             |

---

## 🏗️ Build & Simulate

### 📦 Requirements

* MPLAB IDE with MPASM
* Proteus Design Suite
* PIC16F877A libraries for Proteus

### 🔨 Build

1. Open `Master_CPU` and `CoProcessor` MPLAB projects.
2. Assemble both using MPASM.
3. Verify successful builds and generate HEX files.

### ▶️ Simulate

1. Open `proteus_schematic.pdsprj` in Proteus.
2. Load HEX files for Master and Co-Processor.
3. Run simulation to test system behavior.

---

## 📌 Notes

* PortC is used for data transfer between Master and Co-Processor.
* Master triggers interrupts on Co-Processor for each byte sent.
* Co-Processor acknowledges receipt before next byte.
* System uses 4-bit LCD mode for pin efficiency.

---

## 👥 Team Members

| Name           | Student ID |
| -------------- | ---------- |
| Diana Muzahem  | 1210363    |
| Shahd Abdallah | 1212840    |
| Masa Shaheen   | 1210635    |


---


