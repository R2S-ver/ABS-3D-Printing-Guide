<div align="center">

<img alt="LOGO" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%200.png" width="512" height="512" /> <br>

[English](https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/README.md) | [中文](https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/Chinese/README.md)) <br>

*A practical research log on ABS printing behavior, thermal control, failure analysis, and process optimization.*
> The goal is to document what actually happens during printing, why it happens, and what can be improved in a practical way.

</div>

# Table of Contents
- [1. Overview](#1-overview)
- [2. Research Goal](#2-research-goal)
- [3. Material Background](#3-material-background)
- [4. Test Setup](#4-test-setup)
- [5. Experimental Log](#5-experimental-log)
- [6. Problems Encountered](#6-problems-encountered)
- [7. Possible Solutions](#7-possible-solutions)
- [8. Current Conclusions](#8-current-conclusions)
- [9. Future Work](#9-future-work)
- [10. Self reflection](#10-reflection)
- [10. References](#10-references)
---

## 1. Overview 

Welcome to this research log! <br> 
This repositories documents my experimental journey to understand **ABS filament printing**. ABS is notorious for warping and shrinking, and this study focuses on environmental temperature control, hardware reliability and mitigating "Heat Creep" through a series of tests.

---
## 2. Research Goal

The purpose of this study is to understand ABS printing in a more practical and repeatable way.  
ABS is a material that is often used for functional parts, but it is also known for being more demanding than PLA or other easier materials. Because of that, I wanted to investigate the actual causes behind common printing problems instead of relying only on general advice.

### Main goals of this study
- Observe how ABS behaves under different enclosure temperatures and print conditions.
- Identify the most common failure modes during printing.
- Test how thermal stability affects warping, adhesion, and extrusion reliability.
- Experiment with how changes to different variables affect print quality.
- Build a practical workflow that can later be reused for similar materials.

---

## 3. Material Background

**ABS (Acrylonitrile Butadiene Styrene)** is a widely used engineering thermoplastic known for its toughness, impact resistance, and relatively good heat resistance. Compared with PLA and PETG, it is generally better suited for parts that need stronger mechanical performance, better long-term durability, and improved resistance to higher temperatures.

### ABS vs PLA and PETG

- **PLA** is usually the easiest material to print. It has good surface quality and low warping, but it is less resistant to heat, impact, sunlight and long-term mechanical stress.
- **PETG** sits between PLA and ABS in many cases. It is stronger and more durable than PLA, and it handles moisture and general wear better, but it can still be easier to print than ABS.
- **ABS** is more demanding, but it offers better heat resistance, impact strength, and long-term usability for functional parts.

### Practical differences

- **Service life:** ABS is generally better suited for long-term functional use than PLA, especially when parts are exposed to stress, heat or repeated handling.
- **Resistance to the environment:** ABS usually performs better than PLA in warmer environments and under mechanical load. PETG also performs well, especially where toughness and moderate flexibility are needed.
- **Water resistance:** ABS, PLA, and PETG are all commonly used for parts that may be exposed to moisture, but none of them are truly waterproof by default. Layer adhesion, infill, geometry and post-processing matter a lot. ABS is often preferred when better sealing or post-processing is needed.
- **Material performance:** ABS is typically stronger in heat and more impact-resistant than PLA. PETG is often easier to print than ABS while still offering good toughness, but ABS remains a more challenging material to dial in correctly.

Because of these characteristics, ABS can be seen as a **real test of a consumer FDM printer’s stability and thermal control**. It is not just a material choice, but also a test of whether the machine, enclosure, and slicer settings are balanced well enough for demanding printing conditions.

The filament I use was sponsored by my friend [itsmeyaboi-debug](https://github.com/itsmeyaboi-debug). It have aged during storage and kept in an open space at room temperature(around 22°C) for an extended period, which may have affected its condition. Before printing, it was dried at **65°C for 8 hours** to reduce moisture-related issues.

---

## 4. Test Setup

The following variables were adjusted during the tests:

- Nozzle temperature
- Bed temperature
- Enclosure temperature
- Heater power
- Cooling fan speed
- Print speed
- Glue use
- Build plate cleanliness
- Brim / draft shield use
- Material profile
- Auto temperature control
- Extrusion behavior

### General printer conditions used throughout the study
- ABS filament
- Heated bed
- Enclosure
- Low fan speed
- Cleaned build plate in later tests
- Draft shield / brim in several tests

---

## 5. Experimental Log
<img alt="1" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%201.png" width="512" height="512" /> <br>

### Test 1
- Nozzle: 250°C
- Bed: 100°C
- Heater: off
- Temperature control: manual
- Glue: none
- Ambient temperature: 17°C
- Enclosure temperature: 25°C

<img alt="2" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%202.png" width="1024" height="1024" /> <br>

### Test 2
- Nozzle: 250°C
- Bed: 100°C
- Heater: 750W
- Temperature control: manual
- Glue: none
- Ambient temperature: 16.8°C
- Enclosure temperature: 50–60°C

### Test 1 & 2: ABS printing test
The ABS tests showed that manually controlling the 750W heater led to an extremely unstable enclosure temperature, fluctuating between **36.7°C and 61°C**, which directly explains the failed print after about 40 minutes.

A critical point is that the temperature sensor was mounted high in the ceiling layer, separated from the internal space by a cardboard layer. Because of this, the measured 60°C was likely an underestimate. Since the sensor was closer to the outer wall and cooled down faster, the actual temperature near the bed was probably even higher.

This excessive heat caused **heat creep**, which warmed the hotend cooling path too much and made the filament soften too early inside the extruder, eventually leading to a jam.

To reduce warping without overheating the hardware, the enclosure temperature should be kept constant at around **50–55°C**. The best solution is a **thermostat-controlled outlet** with the sensor placed directly inside the enclosure. A hysteresis of about **5°C** would help eliminate dangerous temperature spikes caused by manual delay.

---
<img alt="3" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%203.png" width="1024" height="1024" /> <br>
### Test 3
#### Hypothesis: thermal equilibrium and part positioning
By reducing heater power to around **400W**, a quasi-stationary thermal balance was achieved. In contrast to the earlier 750W tests, where manual regulation caused strong temperature swings, the enclosure temperature now remained relatively stable between **42°C and 44°C**.

At this point, the average heat input from the heater was approximately equal to the heat loss through the enclosure and small leaks, which reduced large thermal gradients.

This more stable environment reduced the risk of heat creep, because the temperature around the hotend stayed more constant and heat was less likely to travel too far into the heatbreak. As a result, filament feeding remained more reliable and premature softening of the filament was prevented.

During this test, three identical parts were printed at the same time. The middle part remained almost perfect, while the top and bottom parts showed clear warping.

This suggests that the middle position was located in the most thermally stable zone of the enclosure.

Because the parts were partially connected through the brim, they could mechanically influence each other during cooling. As a result, shrink stress was concentrated mainly along the outer edges of the total print area, while the middle part remained in a relatively low-stress zone.

This result suggests that, until the ideal ABS printing temperature of around **50–55°C** is reached, both a stable heat balance and the physical placement of parts inside the printer remain critical.

---
<img alt="4" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%204.png" width="1024" height="1024" /> <br>
### Test 4
- Speed: 100%
- Glue: yes
- Heater: 350W
- Temperature control: manual
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: custom

**Failed reason:** average temperature too low, around **40°C**  
**Consequence:** filament jammed in the upper part of the hotend. The hotend had to be retracted, the jammed section cut off, and the hotend reassembled.

---

### Test 5
- Speed: 50%
- Glue: yes
- Heater: 375W
- Temperature control: manual
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS

**Failed reason:** extrusion check was not performed and the print still failed because of the clog from Test 4.  
However, it was observed that the **375W heater** could maintain a stable temperature of **50–55°C** for an extended period, around 30 minutes.

---

### Test 6
- Speed: 100%
- Glue: yes
- Heater: 370W
- Temperature control: manual
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS

**Failed reason (conjecture):**
- Filament may have been too wet
- Bad glue stick may have caused poor adhesion to the build plate
- Unknown machine failure may have occurred

A full maintenance check was performed, moving parts were lubricated, but the exact cause could not be determined with certainty.

At this point, I want to give up trying on ABS and switching to **PETG or ASA** instead; or purchasing a more reliable and better-known ABS brand like Bambu Lab ABS.

---

<img alt="8" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%208.png" width="512" height="512" /> <br>
**NEW UPGRADE:** The enclosure insulation was upgraded by lining the interior with 10 mm aluminum-coated foam on all four sides and the top. Gaps and seams were sealed with tape to minimize air leakage and prevent airflow. <br>
**NEW UPGRADE:** A thermostat-controlled outlet was also added to automatically regulate temperature.
The heater turns on at 48°C or below and turns off at 51°C or above.
（In practice, after the heater is switched off, the enclosure temperature continues to rise by an additional 2–3°C before gradually cooling down.）<br>
<img alt="5" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%205.png" width="1024" height="1024" /> <br>


### Test 7
- Speed: 100%
- Glue: none
- Heater: 370W
- Temperature control: automatic
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS
- Upgraded isolation: 10mm aluminum-coated foam

This test had a properly controlled enclosure temperature, but a new issue appeared:

**Failed reason (conjecture):**
- The first layer did not stick to the heated bed

This indicated that the remaining problem might not be enclosure temperature alone, but also extrusion reliability and first-layer behavior.

---

### Test 8
- Speed: 50%
- Glue: none
- Heater: 370W
- Temperature control: automatic
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS

This test was part of the continued troubleshooting process. It was used to verify whether reducing speed would improve adhesion and extrusion stability.

---

### Test 9
- Speed: 100%
- Glue: none
- Heater: 370W
- Temperature control: automatic
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS

During this test, the root cause of the earlier failures became clearer.

**Failed reason (conjecture):**
- The extruder gear had insufficient friction and filament powder had accumulated on the gear surface
- The hotend may have been partially clogged, causing excessive extrusion resistance at the start of printing

After manually applying additional extrusion force, printing could continue normally.

### Solution applied
- Manually push the filament about 5 cm inward
- Recover from the partially stuck state
- Resume normal extrusion

**I suspect that the insufficient friction in the extruder may be caused by an excessively high ambient temperature, which leads to the filament softening prematurely in the upstream section of the extruder. As a result, it cannot be reliably fed through to the nozzle.**

<img alt="6" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%206.png" width="1024" height="1024" /> <br>

---

### Test 10
- Speed: 100%
- Glue: none
- Heater: 370W
- Temperature control: automatic
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS

### Test 11
- Speed: 100%
- Glue: none
- Heater: 370W
- Temperature control: automatic
- Fan speed: low
- Build plate: cleaned
- Brim and draft shield: enabled
- Material profile: generic ABS

From **Test 9 onward**, printing became successful and stable.  
In total, **11 tests** were performed: the first **8** failed, and **successful printing began from Test 9**.

---

## 6. Problems Encountered

### Cooling and thermal issues
- Ambient temperature below **45°C** caused warping
- Ambient temperature above **55°C** caused overheating and **70°C** will cause damage to the extruder fan
- Fan speed was too high - set it to 0%
- Bed temperature was not optimal
- Cold air flow required a draft shield
- Unstable enclosure temperature caused thermal swings
- The ambient temperature fluctuates too rapidly
- Passive heat loss is too high

### Extrusion and mechanical issues
- Filament grinding and poor grip on the extruder gear
- Partial clogging in the hotend
- Heat creep
- Overhang cooling was too aggressive
- Filament may have been too wet

### Adhesion issues
- First layer did not stick properly
- Glue did not always improve the result
- Build plate surface needed better cleaning

---

## 7. Possible Solutions

<img alt="7" src="https://github.com/R2S-ver/ABS-3D-Printing-Guide/blob/main/assets/images/ABS%203D%20Printing%20Guide%207.png" width="1024" height="1024" /> <br>

The following solutions/upgrades are possible during the study:

### Hardware and setup improvements
- Buy a new hotend
- Upgrade the enclosure insulation
- Upgrade the build plate
- Buy a thermostat-controlled outlet
- Replace new or upgrade the extruder system

### Process and print settings
- Apply glue for the bed
- Switch from ABS to ASA
- Reduce or increase maximum print speed depending on the test
- Use a custom skirt / draft shield
- Use support rafts if needed
- Clean the build plate carefully before each print
- Reduce cooling fan speed

### Extrusion recovery and reliability
- Manually push the filament forward when the extrusion path becomes partially stuck
- Clear any clog in the hotend before restarting the print
- Check the extruder gear for debris and insufficient grip

### Notes on upgrade the extruder brass gear idea
One idea was to replace the black plastic extruder gear with a brass gear.  
However, this may actually be a **negative optimization** in some cases, because brass can transfer heat more easily and may soften the filament earlier in the feed path. For that reason, the brass gear idea should be treated carefully rather than assumed to be an upgrade.

---

## 8. Current Conclusions

This study showed that ABS printing is not determined by a single factor.  
The result depends on the balance between enclosure temperature, airflow, bed adhesion, print speed, extrusion resistance, and hotend stability.

### Main conclusions
- ABS needs a **stable thermal environment**.
- Manual heating control creates temperature spikes and leads to failure.
- A controlled enclosure temperature around **50–55°C** is much more useful than unstable overheating.
- Heat creep can become a major problem if the enclosure becomes too hot and wraping when too cold.
- First-layer failure may come from extrusion weakness, not only from bed adhesion.
- The extruder gear and hotend condition are just as important as slicer settings.
- From Test 9 onward, the process became stable after the extrusion problem was identified and recovered.

Overall, the study suggests that ABS can be printed successfully at home, but only when the printer is treated as a **system** rather than a single machine setting problem.

---

## 9. Future Work

Further testing could include:

- Comparing ABS with ASA under the same conditions
- Testing a better-quality ABS brand
- Measuring the effect of different enclosure insulation levels
- Testing a more reliable thermostat-controlled heating setup
- Evaluating different build plate materials
- Refining extrusion recovery procedures
- Repeating the same model with different speeds and cooling settings to confirm repeatability

---

## 10. Reflection

This study made me realize that ABS is not just another filament choice. Compared with PLA and PETG, it can be much better suited for parts that need higher heat resistance, better long-term durability, and stronger resistance to repeated stress. In that sense, ABS opens up a range of functional applications that are harder to achieve reliably with PLA or PETG.

At the same time, this project also showed the limits of my testing method. In the early stage, the variables and control groups were not strict enough and several parameters were changed at the same time. To obtain cleaner conclusions in the future, I should ideally test only one variable at a time, even though that would require much more time and patience.

Another important lesson was measurement accuracy. In the first few tests, the temperature sensor was not placed in an ideal position, so the recorded temperature may have been slightly misleading. Starting from Test 7, the sensor probe was moved to about 10 cm above and on the back side of the heated bed. This gave a more accurate reading of the enclosure temperature while avoiding interference with the extruder’s movement.

Overall, this project taught me that material testing is not only about whether a print succeeds or fails. It is also about how well the testing environment is controlled, how reliable the measurements are, and how carefully each variable is isolated.

---

## 11. References
[- Bambulab Basic maintenance](https://wiki.bambulab.com/en/a1/maintenance/basic-maintenance)
