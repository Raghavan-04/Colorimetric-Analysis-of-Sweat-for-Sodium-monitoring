# Colorimetric Analysis of Sweat for Sodium Monitoring with Integrated User Interface

![Project Status](https://img.shields.io/badge/Status-Completed-success) 
![Project Year](https://img.shields.io/badge/Year-November%202025-blue)
![Affiliation](https://img.shields.io/badge/Affiliation-PSG%20College%20of%20Technology-red)

---

##  Project Summary & Clinical Need

This work presents a novel, **strip-based, multimodal biosensing platform** for the **non-invasive, quantitative detection of sodium (Na⁺) in human sweat**. The system is designed for **point-of-care** usability, bridging laboratory-grade precision with portability to enable the early detection of electrolyte imbalance (Hyponatremia/Hypernatremia) and hyperuricemia risk.

The primary innovation is the **Dynamic Environmental Integration**—combining chemical colorimetry with real-time temperature and humidity sensing to mitigate the largest source of error: **sweat sample evaporation.**

##  Core Quantification Model: Kubelka-Munk Theory

Unlike transparent liquid samples which use the Beer-Lambert Law (Absorption), this project utilizes a model for opaque, reflective surfaces (test strips):

*   **Model:** **Kubelka-Munk (K-M) Theory.**
*   **Principle:** The K-M function relates the measured Reflectance (**R**) of the test strip to two key coefficients: Absorption (**K**) and Scattering (**S**).
*   **Key Relationship:** The final sodium concentration is directly proportional to the calculated ratio:
    $$
    \text{Sodium Concentration} \propto \frac{K}{S} = \frac{(1 - R)^2}{2R}
    $$
    The **ESP32** calculates this K/S value from the raw photodiode voltage to achieve robust, scientifically accurate concentration readings.

##  Multi-Modal System Architecture & Signal Chain

The platform integrates optical, electronic, and environmental sensing components to create a unified measurement pipeline.

### 1. Optical Sensing Module (The Core)
| Component | Function | Detail |
| :--- | :--- | :--- |
| **Sensing Platform** | Colorimetric Strip & Sweat Sample | Produces a color change proportional to Na⁺ concentration. |
| **LED-Photodiode Module** | Light Illumination & Reflection Measurement | Precisely aligned LED/Photodiode geometry measures reflected light intensity. |
| **TIA Front End** | Analog Signal Conversion | Converts the low-level electrical current from the Photodiode into a proportional, stable voltage signal. |
| **External ADC** | Digitization | Converts the analog voltage signal into a digital (binary) magnitude for the processor. |

### 2. Processing & Communication
| Component | Function | Detail |
| :--- | :--- | :--- |
| **Processing Unit** | **ESP32 Microcontroller** | Handles real-time data acquisition, signal preprocessing, K/S calculation, and classification against physiological ranges. |
| **Wireless Comm.** | Wi-Fi/BLE | **ESP32** transmits final sodium concentration and environmental data to the Web Dashboard. |

### 3. Environmental Integration (Robustness)
| Sensor | Data Logged | Purpose |
| :--- | :--- | :--- |
| **Temperature/Humidity** | Analog equivalent of ambient conditions. | **Error Flagging:** Logs conditions to explain anomalous high readings (due to evaporation). **Correction:** Provides data for a future advanced correction model. |

---

##  Proposed Real-World Methodology

The final implementation and user-procedure are designed to mitigate real-world errors:

1.  **Preparation & Collection:** User cleans skin patch and collects sweat via absorbent pads/direct strip contact.
2.  **Calibration (Two-Point):** The device performs **Dark Calibration (0% Reflectance)** with the LED off (to zero out electronic noise) and **White Calibration (100% Reflectance)** using a clean strip (to standardize LED brightness).
3.  **Timed Reaction:** The device enforces a precise, pre-programmed incubation time (e.g., 45 seconds) after sample application before taking the reading, controlling for the **Evaporation Challenge**.
4.  **Measurement:** The appropriate color LED (likely Blue) is turned on, and the photodiode measures the reflected voltage ($V_{\text{sample}}$).
5.  **Final Calculation:** The ESP32 calculates the true reflectance ($R$) using the calibrated voltages and plugs this into the K-M equation to determine the final Sodium Concentration.

##  Real-World Challenges and Robustness

The design explicitly addresses the most common sources of inaccuracy in portable biosensors:

| Error Category | Challenge Addressed | Solution/Design Feature |
| :--- | :--- | :--- |
| **Sample/User Errors** | **Evaporation:** Rapid water loss concentrates Na⁺. | **Timed Reaction** programmed into the firmware to ensure consistent incubation. |
| **Optical Errors** | **Ambient Light Leakage:** External light skews readings. | **3D-Printed Custom Enclosure** designed to be light-tight, preventing external light interference (as shown in 3D-Simulation). |
| **Electronic Errors** | **LED Brightness Drift:** LED intensity changes with temperature/age. | **Two-Point Calibration** (Dark/White) performed frequently to normalize the photodiode reading ($R$ is a ratio of voltages). |
| **Calibration Errors** | **Non-Linearity:** The K/S vs. Concentration graph curves at extremes. | The system defines a precise **"Linear Range"** and advises users/systems to only use the linear regression within that range for maximum accuracy. |
| **Chemical Errors** | **Chemical Interference:** Other ions (K⁺, Cl⁻) in sweat. | Rely on the **High Selectivity** of the sodium ionophore reagent on the test strip. |

##  Web-Based User Interface ("Wireless Dashboard")

The ESP32 hosts a lightweight web server and REST API for comprehensive user feedback.

*   **Data Visualization:** Displays real-time sensor data (Colorimetric AU, Temperature, Humidity) and the final calculated **Sodium (Na⁺) concentration**.
*   **Control Panel:** Includes controls for **Start Chart, Stop Chart, Calibrate, and Clean Cycle**.
*   **System Log:** Integrated log panel displays real-time status messages, connection events, and hardware errors from the ESP32, aiding diagnostics.

---

## Forumula 

You're asking to turn that into a **normal formula** — meaning a direct relationship you can implement in code, not just a proportionality.  

Here it is, converted to a practical formula for sodium concentration:

---

## Step 1: Kubelka-Munk function  
From reflectance \( R \):

\[
\frac{K}{S} = \frac{(1 - R)^2}{2R}
\]

---

## Step 2: Calibration (making it a "normal" formula for concentration)  
If sodium concentration \( C \) is proportional to \( K/S \):

\[
C = m \cdot \frac{K}{S} + b
\]

Where:  
- \( m \) = calibration slope  
- \( b \) = calibration intercept  

Substitute \( K/S \):

\[
C = m \cdot \frac{(1 - R)^2}{2R} + b
\]

---

## Step 3: Relating \( R \) to photodiode voltage  

For a reflectance measurement:

\[
R = \frac{V_{\text{sample}}}{V_{\text{reference}}}
\]

Where:  
- \( V_{\text{sample}} \) = voltage from strip  
- \( V_{\text{reference}} \) = voltage from white standard (100% reflectance)

---

## Step 4: Final normal formula for ESP32  

\[
\boxed{C = m \cdot \frac{\left(1 - \frac{V_{\text{sample}}}{V_{\text{ref}}}\right)^2}{2 \cdot \frac{V_{\text{sample}}}{V_{\text{ref}}}} + b}
\]

Where:  
- \( m, b \) = determined by calibration (e.g., linear fit of known standards)  
- All variables are floats

---

## Step 5: ESP32 code example (direct implementation)

```cpp
float getSodiumConcentration(float V_sample, float V_ref, float m, float b) {
    float R = V_sample / V_ref;
    if (R <= 0) return 999.9; // error
    float KS = pow(1 - R, 2) / (2 * R);
    return m * KS + b;
}
```

---

##  Team Members & Faculty Guide

| Role | Name | Roll Number |
| :--- | :--- | :--- |
| **Team Member** | RAGHAVAN | 22L255 |
| **Team Member** | SARRANADHITHIYAA G | 22L262 |
| **Team Member** | SHRIRAM R S | 22L268 |
| **Team Member** | SHYAAMALAN P | 22L270 |
| **Faculty Guide** | Mrs. DEEPIKA J | Assistant Professor, ECE |

**Affiliation:** Electronics and Communication Engineering, PSG College of Technology
