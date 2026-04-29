<div align="center">
<img alt="LOGO" src="https://github.com/R2S-ver/Study-Electronics-Fundamentals/blob/main/assets/images/Banner%202.png" width="256" height="256" />
  
# ABS Printing Thermal Optimization & Reliability Study
[English](README.md) | [中文](README_CN.md)

Welcome to this research log! 
This section documents my experimental journey to master **ABS filament printing**. 
ABS is notorious for warping and shrinking, and this study focuses on environmental temperature control, hardware reliability, and mitigating "Heat Creep" through a series of 11 controlled tests.

*The goal is to achieve a stable, repeatable "Set and Forget" printing process for high-temperature materials.*
</div>

# **Table of Contents**
- [3D Printing Research: ABS Thermal Management](#3d-printing-research-abs-thermal-management) <br>
  1\. [Research Purpose & Goals](#1-research-purpose--goals) <br>
  2\. [Material & Hardware Setup](#2-material--hardware-setup) <br>
  3\. [Experimental Records (Test 1-11)](#3-experimental-records) <br>
  4\. [Problem Analysis & Solutions](#4-problem-analysis--solutions) <br>
  5\. [Final Conclusion](#5-final-conclusion) <br>

---

<details open><summary>

## 🟧 3D Printing Research: ABS Thermal Management
</summary>

<details><summary>

### 🟦 1. Research Purpose & Goals
</summary>

ABS (Acrylonitrile Butadiene Styrene) requires a very specific thermal environment. This research aims to:
- **Solve Warping:** Identify the ideal ambient temperature to prevent part deformation.
- **Prevent Heat Creep:** Balance the internal enclosure temperature to ensure the cold-end of the extruder stays cool enough.
- **Hardware Optimization:** Transition from manual temperature management to an automated, sensor-driven system.
- **Process Reliability:** Move from a high failure rate (>70%) to a stable, successful printing workflow.
</details>

<details><summary>

### 🟦 2. Material & Hardware Setup
</summary>

| Category | Details |
| :--- | :--- |
| **Material** | Generic ABS Filament (Test 1-11) |
| **Printer** | Custom Enclosed FDM Printer |
| **Heating** | 750W / 370W Auxiliary Heater |
| **Control** | Manual control vs. Automatic Thermostat Socket |
| **Safety** | Enclosure with thermal insulation (Cardboard/External layers) |
| **Adhesion** | Glue stick, Brim, and Draft Shields |
</details>

<details><summary>

### 🟦 3. Experimental Records
</summary>

#### **Phase 1: Manual High-Power Tests (The Failure Phase)**
* **Test 1 & 2:** * **Setup:** 750W Heater, Manual Control, No Glue.
    * **Result:** **FAILED.** * **Observation:** Manual control led to extreme fluctuations (36.7°C to 61°C). High heat caused **Heat Creep**, causing filament to jam in the cooling neck. The ceiling sensor (behind cardboard) likely underestimated the actual bed temperature.

#### **Phase 2: Thermal Equilibrium & Positioning**
* **Test 3:**
    * **Setup:** Power reduced to 400W. 
    * **Result:** Semi-stable (42°C - 44°C).
    * **Insight:** Middle parts printed perfectly, while outer parts warped. This proved that the **center of the bed** is the thermal "Sweet Spot." Mechanical stress from cooling concentrated on the outer edges of the linked brims.

#### **Phase 3: Speed & Adhesion Struggles**
* **Test 4 & 5:**
    * **Setup:** 350W-375W Heater, Low fan.
    * **Result:** **FAILED.** * **Reason:** Ambient temp too low (~40°C) leading to jams. Test 5 showed the 375W heater *could* maintain 50-55°C, but a pre-existing clog from Test 4 ruined the run.
* **Test 6:**
    * **Result:** **FAILED.** * **Conjecture:** Wet filament or poor glue adhesion. Decision made to consider PETG/ASA or premium ABS (Bambulab).

#### **Phase 4: Automation & Final Success (The Breakthrough)**
* **Test 7 & 8:**
    * **Setup:** **Auto-temperature control socket (370W)**, No Glue.
    * **Issue:** First layer adhesion failure.
* **Test 9, 10 & 11:**
    * **Setup:** Manual filament force applied at start + Gear cleaning.
    * **Result:** ✅ **SUCCESSFUL.**
    * **Key Discovery:** The root cause was a combination of insufficient extruder gear friction (plastic gear) and a partial initial clog. By manually assisting the first 5cm of extrusion, the "half-stuck" state was cleared, allowing the automated thermal system to finish the job.
</details>

<details><summary>

### 🟦 4. Problem Analysis & Solutions
</summary>

#### **⚠️ Tegengekomen problemen (Identified Issues)**

* **Thermal Control:**
    * Ambient Temp < 45°C causes **Warping**.
    * Ambient Temp > 55°C causes **Overheating/Heat Creep**.
    * Cold air flow causing localized shrinking (Requires **Draft Shield**).
* **Mechanical/Material:**
    * **Filament Grinding:** Gear slipping on the filament.
    * **Heat Creep:** Filament softening too early in the hotend.
    * **Moisture:** Filament too wet, leading to poor structural integrity.
    * **Adhesion:** Inconsistent bed adhesion without proper preparation.

#### **✅ Mogelijke Oplossingen (Proposed Solutions)**

| Solution | Status | Impact |
| :--- | :--- | :--- |
| **Thermostaat stopcontact** | Implemented | **High** - Stabilizes environment |
| **Draft Shield / Skirt layers** | Implemented | **Medium** - Blocks cold drafts |
| **Z-Hop (0.4mm)** | Recommended | **Medium** - Prevents nozzle strikes |
| **Enclosure Insulation** | Planned | **Medium** - Energy efficiency |
| **ASA Filament** | Alternative | **High** - Easier to print than ABS |
| **Extruder Upgrade** | Discussion | **Caution** - Brass gears may increase heat transfer |
| **Lower Print Speed (50%)** | Tested | **Medium** - Improves layer bonding |
</details>

<details><summary>

### 🟦 5. Final Conclusion
</summary>

Through 11 iterations, the research proves that **stability is more important than raw power**. 
1. **Automation is Key:** Switching from a 750W manual heater to a 370W auto-thermostat controlled environment eliminated the thermal spikes that caused heat creep.
2. **The "Sweet Spot":** For ABS, an ambient temperature of **50°C - 55°C** must be maintained.
3. **Starting Resistance:** Many failures attributed to "clogs" were actually due to insufficient gear friction at the start. Manual "priming" or gear maintenance is essential.
4. **Success Rate:** After optimizing these factors, the success rate moved from 0% (Tests 1-8) to **100% (Tests 9-11)**.

#### [>Back to the Table of Contents<](#table-of-contents)
</details>
