# RUNSY — Bilateral Wristband Running Form Coach

> **Status: 🔨 In Progress — Phase 1 (Hardware & Firmware)**

A dual-wristband embedded system that detects bilateral arm swing asymmetry in real time and delivers haptic feedback to correct running form. Built as an EE portfolio project targeting FAE/Technical PM roles at sensor and wearables companies.

---

## The Problem

34% of recreational runners exhibit measurable arm swing asymmetry, which is linked to elevated injury risk and wasted metabolic energy. No consumer wearable currently detects this in real time and gives immediate, personalized corrective feedback — they only show metrics after the fact.

RUNSY solves this: when your arms fall out of sync, the wristband on the offending side vibrates immediately, telling you exactly which arm needs correction.

---

## How It Works

Two wristbands communicate wirelessly during a run. Each has an IMU that tracks arm swing amplitude, timing, and cross-body deviation. A comparison algorithm detects asymmetry relative to your personal baseline — not a generic population average — and triggers haptic + LED feedback on the weaker wrist in real time.

After the run, a companion app shows your symmetry score, form timeline, and fatigue curve.

---

## Hardware

| Component | Role |
|---|---|
| XIAO ESP32-C5 (×2) | Microcontroller + wireless |
| MPU-6050 IMU (×2) | Accelerometer + gyroscope |
| Coin vibration motor 1027 (×2) | Haptic feedback |
| WS2812B NeoPixel LED (×2) | Visual status indicator |
| 2N2222 NPN transistor (×2) | Motor driver circuit |
| LiPo battery (×2) | Untethered operation (Phase 3) |

**Total BOM cost: ~NT$500–700 for Phase 1**

---

## Build Phases

### ✅ Phase 1 — Hardware & Firmware (Weeks 1–5)
- [ ] IMU reading + NeoPixel status indicator
- [ ] Personal baseline calibration routine
- [ ] ESP-NOW wireless link between two boards
- [ ] Bilateral symmetry comparison algorithm
- [ ] Haptic feedback on asymmetry detection
- [ ] Integration test + demo video

### 🔲 Phase 2 — BLE + Companion App (Weeks 6–10)
- [ ] BLE data logging during session
- [ ] React Native app — live data display
- [ ] Post-run symmetry score + form timeline
- [ ] Fatigue curve + session comparison

### 🔲 Phase 3 — Polish & Enclosure (Weeks 11–16)
- [ ] Adaptive personal thresholds (learns across sessions)
- [ ] Session history + improvement tracking
- [ ] 3D printed wristband enclosure
- [ ] LiPo battery integration

---

## Key Technical Concepts

**Symmetry detection:** `ratio = min(leftAmp, rightAmp) / max(leftAmp, rightAmp)` — flag if below personal threshold (default 0.75, adapts over time)

**Wireless protocol:** ESP-NOW for Phase 1 (peer-to-peer, <10ms latency, no router needed) → BLE for Phase 2 (phone connectivity)

**Personalization:** First 2–3 runs establish YOUR baseline symmetric swing. Asymmetry is detected relative to your pattern, not a population average — scientifically justified since optimal form varies by individual.

**IMU axes used:**
- Y-axis accelerometer → swing amplitude (forward/back)
- X-axis accelerometer → cross-body deviation (lateral waste)
- Z-axis gyroscope → swing cadence/timing

---

## Research Backing

- Active arm swing reduces metabolic cost of running by ~5% vs. fixed arms *(2025 study)*
- One restrained arm increases frontal plane knee/hip loading — direct injury risk link
- 34% of recreational runners run below the 90% symmetry threshold associated with elevated injury risk
- Individual asymmetry patterns vary, making personal baseline detection more accurate than population averages

---

## Career Context

This project maps directly to:
- **FAE roles** at sensor suppliers (Bosch Sensortec, STMicro, TDK, Qualcomm) — customers integrate the same MPU-6050/MAX30102 stack
- **Technical PM roles** at wearables OEMs — demonstrates hardware tradeoff thinking, UX design for body-worn devices, end-to-end system ownership

Future expansion: add smart glasses IMU as a third sensor node for head motion tracking during running.

---

## Repo Structure
```
RUNSY/
├── phase1_firmware/
│   ├── wristband_left/       # ESP32-C5 firmware — left wristband
│   └── wristband_right/      # ESP32-C5 firmware — right wristband
├── phase2_app/               # React Native companion app (coming Phase 2)
├── hardware/                 # Wiring diagrams, schematics
├── research/                 # Biomechanics data and references
└── docs/                     # Build log, photos, demo videos
```

---

## Author

**Cheng Wei (Alex) Kao** — B.S. Electrical Engineering, UCLA '28  
[LinkedIn](https://linkedin.com/in/your-link-here) · [weiweikao1018@gmail.com](mailto:weiweikao1018@gmail.com)
