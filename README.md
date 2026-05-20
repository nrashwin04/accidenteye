# 🚨 AccidentEye — Real-Time Road Accident Detection & Alert System

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-orange.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-green.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-red.svg)
![Status](https://img.shields.io/badge/Status-Work%20In%20Progress-yellow.svg)

---

## What I'm building

AccidentEye is an end-to-end computer vision system designed to detect road accidents in real time from dashcam or CCTV footage, classify accident severity, and automatically trigger alerts with the incident frame and timestamp.

The goal is to build something that could realistically be deployed at traffic monitoring stations or integrated into dashcam hardware — not just a demo that works on clean dataset images.

---

## The problem

Road accident response time is a critical factor in saving lives. Most accident detection today is either manual (someone watching CCTV) or relies on impact sensors in vehicles. A vision-based system that can watch multiple feeds simultaneously and alert authorities immediately has real-world value — and is an active research problem.

---

## How I aim to build it

### Detection
Fine-tune YOLOv8 on a custom-curated dataset of dashcam and traffic camera footage, labelled specifically for accident detection across varied lighting, weather, and road conditions in India.

### Severity Classification
A secondary EfficientNet-B0 classifier that takes the detected accident region and classifies it as Minor or Major based on visible vehicle damage, position, and surrounding context.

### Temporal Confirmation
A single-frame detection is unreliable. I aim to implement a temporal confirmation mechanism — an accident is only flagged when detected across multiple consecutive frames — dramatically reducing false positives.

### Object Tracking
ByteTrack integration to maintain persistent vehicle IDs across frames, enabling the system to track which vehicles were involved in a detected incident.

### Alerting Pipeline
On confirmed accident detection, the system triggers:
- WhatsApp alert with the incident frame and severity
- Email notification with timestamp and location metadata
- Logging to a local database for review

### API & Deployment
A FastAPI backend serving predictions via REST endpoints, with a Streamlit frontend for live video analysis and alert configuration. Fully containerised with Docker.

---

## Planned tech stack

| Component | Technology |
|---|---|
| Object detection | YOLOv8 (Ultralytics) |
| Severity classification | EfficientNet-B0 (PyTorch) |
| Object tracking | ByteTrack via Supervision |
| Backend API | FastAPI + Uvicorn |
| Frontend | Streamlit |
| Alerting | Twilio (WhatsApp) + SMTP |
| Experiment tracking | Weights & Biases |
| Dataset management | Roboflow |
| Containerisation | Docker |

---

## Dataset

I am curating a custom dataset combining:
- CADP (Car Accident Detection and Prediction dataset)
- Dashcam footage collected and labelled manually
- Augmented with Roboflow — rotation, brightness variation, horizontal flip

Target: 1000+ labelled accident frames across varied conditions.

---

## Current status

| Component | Status |
|---|---|
| Dataset collection | 🔧 In progress |
| YOLOv8 baseline training | ⏳ Not started |
| Severity classifier | ⏳ Not started |
| Temporal confirmation | ⏳ Not started |
| Alert system | ⏳ Not started |
| FastAPI backend | ⏳ Not started |
| Streamlit frontend | ⏳ Not started |
| Docker deployment | ⏳ Not started |

---

## Run locally (once complete)

```bash
git clone https://github.com/nrashwin04/accidenteye.git
cd accidenteye
pip install -r requirements.txt
cp .env.example .env  # fill in Twilio and email credentials
uvicorn app.main:app --reload
# visit http://localhost:8000/docs
```

---
