# POT Angle Calibration Lab

## Overview

This page provides a complete learning module for teaching potentiometer (POT) angle measurement using ESP32 and a physical paper dial. Students will learn analog sensing, ADC interpretation, calibration, linear mapping, and real‑world alignment between physical rotation and digital measurement.

---

## Learning Goals
- Understand how a potentiometer works as a variable resistor.
- Read analog values using ESP32 ADC.
- Create a physical angle dial using paper.
- Collect calibration data for minimum and maximum ADC values.
- Map ADC readings to real angles using linear transformation.
- Validate accuracy by comparing physical and digital angles.

---

## Materials
- Potentiometer (10k recommended)
- ESP32 development board
- Jumper wires
- Breadboard (optional)
- A4 paper or cardboard
- Pen, ruler, protractor
- Tape or glue

---
## Step 1: Create the Paper Angle Dial
1. Draw a circle approximately 10–12 cm in diameter.
2. Mark the center point clearly.
3. Use a protractor to draw angle markings:
    - 0° at the rightmost horizontal
    - 45°, 90°, 135°, 180°
    - Optionally extend to 270° and 300° if the POT supports wider rotation
4. Label each angle clearly.
5. Mount the POT so its shaft aligns exactly with the center of the circle.
6. Attach a pointer to the POT knob (paper arrow or plastic pointer).

---

## Step 2: Wiring the POT to ESP32
- Connect POT **left pin** → 3.3V
- Connect POT **right pin** → GND
- Connect POT **middle pin** → ESP32 ADC pin (e.g., GPIO 34)

---
## Step 3: Read ADC Values

Use this minimal ESP32 code to read raw ADC values:
```
int adc = analogRead(34);
Serial.println(adc);
```
Record ADC values at several known angles.
---
## Step 4: Collect Calibration Data
Rotate the POT to match the paper dial angles and record ADC values.
Example table:

| Angle (°) | ADC Value |
| --------- | --------- |
| 0         | 180       |
| 45        | 1100      |
| 90        | 2100      |
| 135       | 3000      |
| 180       | 3900      |

Identify:
- **ADC_min** = value at 0°
- **ADC_max** = value at max angle
- **θ_max** = total rotation angle (usually 180°)

---
## Step 5: Compute Linear Mapping
Use the linear transformation formula:
```
angle = (ADC - ADC_min) / (ADC_max - ADC_min) * θ_max
```
Example:
- ADC_min = 180
- ADC_max = 3900
- θ_max = 180°
Mapping:
```
angle = (ADC - 180) * 180.0 / 3720.0;
```

---
## Step 6: ESP32 Real‑Time Angle Display

Full example code:
```
int adc = analogRead(34);
float angle = (adc - 180) * 180.0 / 3720.0;

Serial.print("ADC = ");
Serial.print(adc);
Serial.print("  Angle = ");
Serial.println(angle);
```

Students should rotate the POT and compare:
- Physical pointer angle
- ESP32 computed angle

---
## Step 7: Accuracy Check
Ask students to test at random angles:
- Predict angle using ESP32
- Compare with paper dial
- Note error in degrees

If error is large:
- Re‑measure ADC_min and ADC_max
- Check pointer alignment
- Consider piecewise calibration if POT is non‑linear

---
## Extensions
- Create a 270° or 300° dial if POT supports wider rotation.
- Add OLED display to show angle.
- Log angle data over time.
- Use piecewise linear mapping for improved accuracy.

---
## Key Takeaways
- POT provides a simple, intuitive analog input.
- Calibration is essential for accurate measurement.
- Linear mapping connects physical rotation to digital values.
- Students gain hands‑on understanding of sensor behavior and edge computing.