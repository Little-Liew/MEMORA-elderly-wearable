# Memora: Smart Elderly Safety & Legacy Wearable Ecosystem

Memora is an open-source IoT safety companion designed to provide continuous health telemetry, fall detection, geofencing, and digital memory preservation for elderly individuals and dementia patients.

---

## 1. System Architecture Overview
[ Wearable Hardware ]
├── ESP32 Microcontroller (Core Logic & BLE/Wi-Fi)
├── MPU6050 (Accelerometer/Gyroscope for Fall Detection)
├── MAX30102 (PPG Heart Rate & SpO2)
├── MLX90614 (Contactless Skin Temperature)
├── NEO-6M (GPS Telemetry)
└── Physical SOS Button + Tamper-Resistant Casing
│
▼ (MQTT / HTTP JSON Payload)
[ Backend Cloud API ]
├── Ingestion Endpoint
├── Automated Escalation Logic (Caregiver Call -> Hospital Webhook)
└── Encrypted Memory Diary Storage (S3 / DynamoDB)
│
▼
[ Mobile Application ]
├── Caregiver Live Health & Geofence Dashboard
└── Legacy Diary & Memory Capsules

---

## 2. Hardware Pinout & Module Specification

| Sensor / Component | Model | Protocol / Interface | Default Address / GPIO |
| :--- | :--- | :--- | :--- |
| **MCU** | ESP32-WROOM-32 | - | Main Controller |
| **Fall / Motion** | MPU6050 | I2C | `0x68` (SDA: GPIO 21, SCL: GPIO 22) |
| **Heart Rate / SpO2**| MAX30102 | I2C | `0x57` (SDA: GPIO 21, SCL: GPIO 22) |
| **Thermal Sensor** | MLX90614 | I2C | `0x5A` (SDA: GPIO 21, SCL: GPIO 22) |
| **GPS Module** | NEO-6M | UART | TX -> GPIO 16 (RX2), RX -> GPIO 17 (TX2) |
| **SOS Trigger** | Push Button | Digital In | GPIO 4 (Pull-Up) |
| **Buzzer / Alarm** | Passive Buzzer | PWM / Digital | GPIO 18 |

---

## 3. Data Telemetry Schema

json
{
  "device_id": "MEMORA-MY-001",
  "timestamp": 1714500000,
  "vitals": {
    "heart_rate_bpm": 76,
    "spo2_percent": 98,
    "skin_temp_c": 36.6
  },
  "location": {
    "lat": 5.3556,
    "lng": 100.3025,
    "in_safe_zone": true
  },
  "status": {
    "fall_detected": false,
    "sos_triggered": false,
    "battery_level_percent": 84
  }
}


## 4. Emergency SOS Escalation WorkflowTrigger: 
Hardware registers an impact ($SVM > 2.5g$ + horizontal inactivity) or user presses SOS.  Phase 1 Alert: Backend initiates an automated push alert and phone call to the primary linked caregiver[cite: 1].Phase 2 Escalation: If the alert remains unacknowledged for 60 seconds, dispatch coordinates directly to designated emergency medical services / community home staff[cite: 1].5. Development Roadmap for Contributors[ ] Implement complementary filter and SVM thresholding for MPU6050 fall detection[cite: 1].[ ] Implement deep sleep states on ESP32 to optimize Li-Po battery endurance[cite: 1].[ ] Build Flutter/React Native front-end using the UI wireframes in /docs[cite: 1].[ ] Finalize 3D printable/injection mold CAD files for the tamper-resistant lock[cite: 1].

---

## Attribution & Project Background
Originally conceptualized and documented by Team Memora at Universiti Sains Malaysia (USM)[cite: 1].

Released under the MIT Open Source License for open research, university student capstones, and community eldercare non-profit innovation[cite: 1].
