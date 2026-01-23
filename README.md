# Colorimetric Analysis of Sweat for Sodium Monitoring with Integrated User Interface

![Project Status](https://img.shields.io/badge/Status-Completed-success) 
![Project Year](https://img.shields.io/badge/Year-November%202025-blue)
![Affiliation](https://img.shields.io/badge/Affiliation-PSG%20College%20of%20Technology-red)

**Project Name:** Colorimetric Analysis of Sweat for Sodium Monitoring with Integrated User Interface
**Course:** 19L720 - PROJECT WORK 1
**Batch Number:** 19

---

## 💡 Project Summary & Clinical Significance

This project presents a novel, strip-based, **multi-modal biosensing platform** for the non-invasive, quantitative detection of **sodium (Na⁺) in human sweat**. The primary goal is to bridge the gap between laboratory-grade precision and point-of-care usability to enable early detection of electrolyte imbalance (Hyponatremia/Hypernatremia) and associated risks.

### Clinical Need & Impact
*   **Hyponatremia/Hypernatremia:** These are common electrolyte disorders affecting high-risk populations (elderly, chronic illness patients) with mortality rates as high as **40% to 60%** in severe cases.
*   **Non-Invasive Diagnostics:** Sweat monitoring offers a real-time, painless, and continuous alternative to traditional blood sampling.
*   **Target:** The system directly addresses the need for a **low-cost, portable solution** for tracking at-risk individuals outside the hospital.

## 📐 Multi-Modal Biosensing Platform Architecture

The system is built on a **colorimetric sensing platform** that uses an optical module integrated with environmental sensing to correct for real-world inaccuracies.

### 1. Optical Sensing Module (The Core)
*   **Method:** **Sodium Paper-Strip Colorimetry.** Sweat samples cause a color change on the strip proportional to the Na⁺ concentration.
*   **Hardware:** A dedicated **LED-Photodiode Optical Module** with precisely aligned geometry illuminates the strip and measures the reflected light intensity.
*   **Quantification Theory:** The system utilizes the **Kubelka-Munk (K-M) theory** to convert the measured light Reflectance (R) into an equivalent Absorption value (K/S), which is directly proportional to the sodium concentration.

### 2. Signal Processing & Quantification
*   **Signal Conversion:** The electrical signal from the photodiode is converted into a stable Voltage Signal via a **TIA Front End** (Transimpedance Amplifier).
*   **Digitization:** The voltage is fed into an **External ADC** (Analog-to-Digital Converter) to produce a magnitude in binary.
*   **Processing Unit:** An **ESP32 Processing Unit** handles real-time data acquisition and pre-processing.
*   **Quantification:** Processed digital values are mapped to a final Na⁺ concentration (in mmol/L) using **Calibration Models** developed from synthetic sweat standards.

### 3. Environmental Integration (Novelty)
*   **Component:** Environmental Sensors (Temperature and Humidity Sensors).
*   **Purpose:** The novelty lies in combining colorimetry with live environmental data to address the biggest real-world error source: **sweat sample evaporation** (which falsely concentrates the sodium).
*   **Future Functionality:** The environmental data enables **Error Flagging** for anomalous readings and can be used to apply an **Advanced Correction Factor** to compensate for estimated evaporative loss.

## ✨ Project Objectives & Goals

| Category | Goal |
| :--- | :--- |
| **Integration Challenge** | Develop a compact **LED-photodiode optical system** that minimizes cross-interference and maintains quantitative accuracy for sodium sensing. |
| **Performance Goals** | Achieve high sensitivity and specificity for sodium within physiological ranges, comparable to clinical laboratory standards, enabling rapid, real-time analysis. |
| **Clinical Translation** | Deliver a **portable, user-friendly diagnostic device** suitable for non-invasive, point-of-care testing outside specialized laboratories. |
| **Economic Impact** | Reduce overall diagnostic costs by replacing bulky, multi-instrument setups with a single low-cost, integrated, and scalable platform. |

## 🌐 Web-Based User Interface (Wireless Dashboard)

The project includes an integrated user interface for real-time visualization:
*   **Web Technologies:** Dynamic dashboard built using **HTML, CSS, and JavaScript**.
*   **Connectivity:** The UI communicates with the **ESP32** via a **REST API** (`/api/sensors`, `/api/status`) hosted directly on the microcontroller.
*   **Real-Time Visualization:** Enables live data display of Colorimetric (AU), Temperature (°C), and Humidity (%).
*   **Robustness Features:** Implements a **System Log Panel** to display real-time hardware errors and a **"heartbeat" system** to automatically detect and report connection loss.

## 🛠️ Feasibility and Future Scope

*   **Feasibility:** Confirmed using low-cost, readily available components like the **ESP32** and standard optical components (Photodiode, LEDs).
*   **Extended Scope (Future):** Expansion with additional sensing modalities (electrochemical sensors), Machine Learning for decision support, and miniaturization into a dedicated wearable/point-of-care device.

---

## 🧑‍💻 Team Members & Guide

| Role | Name | Roll Number |
| :--- | :--- | :--- |
| **Team Member** | RAGHAVAN | 22L255 |
| **Team Member** | SARRANADHITHIYAA G | 22L262 |
| **Team Member** | SHRIRAM R S | 22L268 |
| **Team Member** | SHYAAMALAN P | 22L270 |
| **Faculty Guide** | Mrs. DEEPIKA J | Assistant Professor, ECE |

**Affiliation:** Electronics and Communication Engineering, PSG College of Technology
