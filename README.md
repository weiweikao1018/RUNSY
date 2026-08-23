# RUNSY 🏃
**Dual Wristband Running Form Coach**

Detects bilateral arm swing asymmetry in real time using IMU sensors and provides haptic + LED feedback to correct running form.

---

## Problem
Most runners develop asymmetric arm swing without knowing it — one arm crosses the body, one swings too wide. This wastes energy and increases injury risk. No affordable wearable device targets this specific issue.

## Solution
Two wristbands (ESP32-C5 + MPU-6050) communicate wirelessly via ESP-NOW. Each measures arm swing magnitude. If the difference exceeds a threshold, an LED and vibration motor alert the runner in real time.

---

## Hardware BOM

| Component | Qty | Est. Cost |
|---|---|---|
| Seeed XIAO ESP32-C5 | 2 | $8 each |
| GY-521 MPU-6050 IMU | 2 | $3 each |
| RGB LED (common cathode) | 2 | $0.50 each |
| Vibration Motor (ERM) | 2 | $2 each |
| 330Ω Resistors | 6 | $0.10 each |
| LiPo Battery 3.7V 500mAh | 2 | $8 each |
| Breadboard + Wires | — | $5 |

---

## Build Phases

### Phase 1 — Hardware + Firmware (Weeks 1–5)
- [x] **Week 1**: Single IMU reading + RGB LED status indicator ✅
  - MPU-6050 reads accelerometer via I2C (`Wire.begin()` default pins)
  - LED: green = still, blue = moving, red = shaking
  - Thresholds tuned to actual sensor output (1.30 / 1.70 g)
- [ ] **Week 2**: Add gyroscope data + arm swing pattern detection
- [ ] **Week 3**: Second board + ESP-NOW bilateral communication
- [ ] **Week 4**: Symmetry algorithm (`|leftMag - rightMag| > threshold`)
- [ ] **Week 5**: Vibration motor haptic feedback

### Phase 2 — BLE + Mobile App (Weeks 6–10)
- [ ] BLE data streaming to phone
- [ ] React Native companion app
- [ ] Session logging + symmetry score display

### Phase 3 — Polish (Weeks 11–16)
- [ ] 3D printed enclosure
- [ ] Battery management + charging circuit
- [ ] User testing with runners

---

## Symmetry Detection Formula

```
asymmetry = |leftMagnitude - rightMagnitude|

if asymmetry < 0.2  → green  (good form)
if asymmetry < 0.5  → blue   (slight asymmetry)
if asymmetry > 0.5  → red    (correct your form)
```

Where magnitude = √(ax² + ay² + az²) in g-force units.

---

## IMU Axes (MPU-6050 on wrist)

- **X**: Forward/backward swing direction
- **Y**: Side-to-side (crossing body = bad form)
- **Z**: Up/down bounce

---

## Key Technical Notes

- Use `Wire.begin()` without pin arguments on XIAO ESP32-C5 (default pins work; specifying GPIO 6/7 explicitly causes I2C errors)
- Use `Wire.endTransmission(false)` + read 14 bytes (full burst) for reliable MPU-6050 reads
- RGB LED wiring: B G R — (common cathode), 330Ω on each pin
- R and G pins may be physically swapped depending on LED — verify with `setColor()` test

---

## Research Backing

- Arm swing asymmetry linked to 23% higher metabolic cost (Journal of Biomechanics, 2019)
- Wearable IMU-based gait analysis validated vs. lab motion capture (Sensors, 2020)

---

## Repo Structure

```
RUNSY/
├── RUNSY_week1/
│   └── RUNSY_week1.ino    ← Week 1: IMU + LED (complete)
├── RUNSY_README.md
```

---

## Career Context

Built by Cheng Wei Kao (UCLA EE, 2027) as a portfolio project targeting FAE / Technical PM roles at sensor and wearables companies (Bosch Sensortec, STMicro, TDK, Qualcomm).

GitHub: https://github.com/weiweikao1018/RUNSY
