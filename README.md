# Simulated ECG Signal Generator & Peak Analyzer (BME 495)

## Overview
This repository contains an independent, software-based LabVIEW Virtual Instrument (VI) created for **BME 495**. 

Rather than acquiring hardware signals through physical electrodes and DAQ boards, this project **programmatically synthesizes** an ECG waveform in software using custom 1D array sequences and defined sample timing (dt = 0.01 s). It provides a reliable, reproducible environment to perform real-time amplitude feature extraction (Peak-to-Peak and Positive Peak) and graph cursor measurements without requiring physical test hardware or human subject data.

---

## Technical Specifications & Dataset Parameters

Rather than loading an external database (e.g., PhysioNet), the ECG waveform is synthesized programmatically using a custom numerical array and time-step configuration.

### 1. Signal Array Data (`Y` Values)
The baseline voltage and cardiac deflection points are defined as follows:

| Point Index | Value (V) | Feature Description |
| :---: | :---: | :--- |
| `0` | `1.0` | Isoelectric Baseline |
| `1` | `1.3` | **P Wave** (Atrial Depolarization) |
| `2` | `1.0` | Baseline Return |
| `3` | `1.0` | PR Segment |
| `4` | `0.8` | **Q Wave** (Initial Ventricular Deflection) |
| `5` | `2.5` | **R Peak** (Ventricular Depolarization) |
| `6` | `0.7` | **S Wave** (Ventricular Depolarization) |
| `7` | `1.1` | ST Segment Baseline |
| `8` | `1.5` | **T Wave** (Ventricular Repolarization) |
| `9` | `1.1` | Baseline Return |

### 2. Time Base Configuration (`dt`)
- **Sampling Interval (dt):** 0.01 s (10 ms)
- **Sampling Rate (Fs):** 100 Hz (1 / dt)
- **Time Calculation:** t[i] = t_0 + (i * dt)

---

## System Architecture

1. **Software Waveform Synthesis:** The `normal` 1D array is passed into the `Build Waveform` function along with dt = 0.01 s to build a continuous native LabVIEW waveform cluster.
2. **Measurement Processing:** The waveform cluster routes into the `Amplitude and Level Measurements` Express VI:
   - **Positive Peak:** Extracts the maximum voltage value (2.5 V).
   - **Peak-to-Peak:** Calculates total signal span (2.5 V - 0.7 V = 1.8 V).
3. **Data Visualization:** Signal output streams directly to both a **Waveform Graph** (for frame-by-frame cursor inspection) and a **Waveform Chart** (for continuous scrolling observation).

---

## System Screenshots

### Front Panel Interface
*Displays the live simulated ECG waveform, interactive measurement cursors, and peak measurement displays.*

<img width="1238" alt="Front Panel Interface" src="https://github.com/user-attachments/assets/fce97df5-2351-4cc0-a60a-1601c85fbe10" />

### Block Diagram & Wiring Logic
*Shows the program flow connecting array generation, waveform construction, amplitude measurement blocks, and visual indicators.*

<img width="732" alt="Block Diagram Logic" src="https://github.com/user-attachments/assets/29ab67f7-b982-4f8f-8af6-df12fe26e9bc" />

---

## How to Run (No Hardware Required)

1. Clone this repository:
   ```bash
   git clone [https://github.com/Siddhav24/Simulated-Labview-ECG.git](https://github.com/Siddhav24/Simulated-Labview-ECG.git)
