<div align="center">

<br>

# `Ala Mahlak`

#### على مهلك

<br>

**Real-Time AI-Powered Driver Monitoring System**

Detecting drowsiness and distraction before they become accidents.

<br>

[![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)](#)
[![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat-square&logo=dart&logoColor=white)](#)
[![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)](#)
[![.NET](https://img.shields.io/badge/.NET-512BD4?style=flat-square&logo=dotnet&logoColor=white)](#)
[![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=csharp&logoColor=white)](#)
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](#)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)](#)
[![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)](#)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white)](#)

<br>

---

</div>

<br>

## About

**Ala Mahlak** (على مهلك — *"Take it easy / Slow down"*) is an intelligent driver monitoring system that uses **computer vision** and **deep learning** to detect distracted and drowsy driving in real time.

The system pairs a **mobile application** — which monitors the driver through the phone's camera — with a **web dashboard** — where fleet managers track performance, review trips, and generate safety reports.

> **What makes it different?** Traditional driver monitoring systems cost thousands per vehicle and require specialized infrared cameras and hardware installation. Ala Mahlak runs entirely on a **standard smartphone camera** — making it affordable, portable, and deployable at scale across developing markets where no DMS solutions exist today.

<br>

## The Problem

<table>
<tr>
<td width="50%">

### The Numbers

- **42,915** traffic fatalities in 2021 alone (NHTSA)
- **10.5%** year-over-year increase — largest in recorded history
- Drowsy driving **drastically reduces** reaction time and awareness
- Drivers consistently **overestimate** their own alertness
- Human error remains the **#1 cause** of road accidents

</td>
<td width="50%">

### Why Existing Solutions Fall Short

- **Expensive** — IR sensors, edge-AI chips, vehicle integration
- **Hardware-locked** — Can't retrofit older vehicles or scale to fleets
- **No MENA support** — Trained on European/US data; fail under harsh sun, diverse faces, cultural clothing
- **Reactive only** — Detect fatigue after the fact, never predict it
- **Privacy-invasive** — Always-on face recording with no local processing

</td>
</tr>
</table>

<br>

## Architecture

```
                                    ┌──────────────────────┐
                                    │                      │
                                    │     AI  Server       │
                                    │  ┌────────────────┐  │
                     Camera Feed    │  │  P-YOLOv8      │  │    Detection
    ┌──────────┐  ─────────────── > │  │  Distraction   │  │ ─────────────── >  Visual & Audio
    │          │                    │  │  Detection      │  │                    ALERTS
    │  Mobile  │                    │  ├────────────────┤  │
    │   App    │                    │  │  DMD Pipeline   │  │
    │ (Flutter)│  < ─────────────── │  │  Drowsiness    │  │
    │          │    Alerts + Report │  │  Detection      │  │
    └────┬─────┘                    │  └────────────────┘  │
         │                          │                      │
         │                          └──────────┬───────────┘
         │                                     │
         │  Trip Data                          │  Analytics
         v                                     v
    ┌──────────┐                    ┌──────────────────────┐
    │          │                    │                      │
    │ Backend  │ < ──────────────── │    Web Dashboard     │
    │  API     │ ────────────────>  │      (React)         │
    │(.NET/C#) │   Fleet Reports   │                      │
    │          │                    │                      │
    └──────────┘                    └──────────────────────┘
```

<table>
<tr>
<td><strong>1. Capture</strong></td>
<td>The mobile app streams real-time video from the smartphone's front camera</td>
</tr>
<tr>
<td><strong>2. Analyze</strong></td>
<td>Frames are processed by the AI server — P-YOLOv8 classifies distraction behaviors, DMD pipeline detects drowsiness signs (eye closure, yawning, gaze)</td>
</tr>
<tr>
<td><strong>3. Alert</strong></td>
<td>Unsafe behavior triggers <strong>instant visual and audio alerts</strong> within 1 second</td>
</tr>
<tr>
<td><strong>4. Report</strong></td>
<td>Trip data, detection events, and safety metrics flow to the web dashboard for fleet managers</td>
</tr>
</table>

<br>

## AI & Detection

<div align="center">

### Core Models

</div>

<table>
<tr>
<th width="25%">Model</th>
<th width="20%">Task</th>
<th width="55%">Details</th>
</tr>
<tr>
<td>

**P-YOLOv8**
<br>
<sub>Pruned YOLOv8n-cls</sub>

</td>
<td>

Distraction Classification

</td>
<td>

Compact, real-time classification of distracted driving behaviors — texting, eating, talking on phone, reaching behind, and more. Optimized through pruning for edge deployment.

- **Accuracy:** 99.46%
- **Inference:** 12.9 ms (~77 FPS)
- **Size:** 2.84 MB / ~1.45M parameters
- **Dataset:** State Farm Distracted Driver Detection (10 distraction classes)

</td>
</tr>
<tr>
<td>

**DMD Pipeline**
<br>
<sub>MTCNN + MobileNetV3</sub>

</td>
<td>

Drowsiness & Gaze Detection

</td>
<td>

Multi-stage pipeline using the DMD (Driving Monitoring Dataset) approach — face detection and alignment via MTCNN, followed by gaze estimation and occlusion-aware drowsiness detection using MobileNetV3-Small.

- **Accuracy:** 99.70% (occlusion), 86.3% (gaze)
- **Modality:** RGB + IR capable
- **Strength:** Handles low-light, partial occlusions (masks, sunglasses, hands)
- **Dataset:** DMD — multimodal RGB/IR dataset with real-world driving conditions

</td>
</tr>
</table>

<br>

## Features

<table>
<tr>
<td width="50%" valign="top">

<div align="center">

### Mobile App
**For Drivers**

</div>

<br>

| | Feature |
|:--|:--------|
| **Detection** | Real-time drowsiness & distraction monitoring |
| **Alerts** | Instant visual and audio warnings |
| **Trips** | Start/end trips with automatic AI monitoring |
| **History** | Review past trips and detection events |
| **Company** | Request to join a fleet / accept invitations |
| **Chat** | In-app messaging with fleet admins |
| **Profile** | Account management & password recovery |

</td>
<td width="50%" valign="top">

<div align="center">

### Web Dashboard
**For Fleet Managers**

</div>

<br>

| | Feature |
|:--|:--------|
| **Overview** | Enterprise dashboard with safety analytics |
| **Monitoring** | Track all company drivers and their trips |
| **Reports** | Review trip reports with detection breakdowns |
| **Drivers** | Approve/reject requests, send invitations |
| **Management** | Add or remove drivers from company fleet |
| **Admins** | Create and manage admin accounts |
| **Access** | Role-based control (Driver, Admin, Company) |

</td>
</tr>
</table>

<br>

## Performance Targets

<div align="center">

| Metric | Target |
|:-------|:------:|
| Detection Latency | `< 500 ms` per frame |
| Alert Response | `< 1 sec` from detection |
| AI Accuracy | `>= 95%` for drowsiness & distraction |
| Mobile Footprint | `<= 20% CPU`  `<= 200 MB RAM` |
| Dashboard Load | `< 3 sec` for 100 concurrent users |
| Scale | `10K` enterprise users / `100K` drivers |
| Security | `TLS/AES` encryption, GDPR-compliant |

</div>

<br>

## Tech Stack

<table>
<tr>
<th width="20%">Layer</th>
<th width="30%">Technologies</th>
<th width="50%">Purpose</th>
</tr>
<tr>
<td><strong>Mobile</strong></td>
<td>Flutter, Dart</td>
<td>Cross-platform driver app — camera capture, real-time alerts, trip management</td>
</tr>
<tr>
<td><strong>Web</strong></td>
<td>React, JavaScript</td>
<td>Admin dashboard — fleet monitoring, analytics, driver management</td>
</tr>
<tr>
<td><strong>Backend</strong></td>
<td>.NET, C#, ASP.NET</td>
<td>RESTful API — authentication, role management, database operations, secure communication</td>
</tr>
<tr>
<td><strong>AI/ML</strong></td>
<td>Python, PyTorch, OpenCV</td>
<td>Deep learning inference — P-YOLOv8 distraction detection, DMD drowsiness pipeline</td>
</tr>
<tr>
<td><strong>Database</strong></td>
<td>SQL Server</td>
<td>Relational storage — users, companies, trips, reports, aggregate analytics</td>
</tr>
<tr>
<td><strong>Training</strong></td>
<td>Google Colab (GPU/TPU)</td>
<td>Cloud-based model training and experimentation</td>
</tr>
</table>

<br>

## Timeline

```
 Sep 2025                                                              May 2026
  │                                                                       │
  │  Planning &         System            Backend            Integration  │
  │  Requirements       Design            Development        & Testing    │
  │  ┌─────────┐    ┌───────────┐    ┌──────────────────┐   ┌─────────┐  │
  │  │ Phase 1 │───>│  Phase 2  │───>│     Phase 3      │──>│ Phase 6 │  │
  │  └─────────┘    └───────────┘    └──────────────────┘   └────┬────┘  │
  │                       │                                      │       │
  │                       │    AI Model Development & Training   v       │
  │                       │    ┌─────────────────────────────────────┐   │
  │                       └───>│            Phase 4                  │   │
  │                            └─────────────────────────────────────┘   │
  │                                          │                           │
  │                                          │  Mobile & Web Development │
  │                                          │  ┌──────────────────┐     │
  │                                          └─>│     Phase 5      │──> Deploy
  │                                             └──────────────────┘     │
  │                                                                      │
  Sep        Oct        Nov       Dec    Jan    Feb    Mar    Apr       May
```

<div align="center">

**9.75 months** — September 2025 to May 2026

</div>

<br>

## Repositories

| Repository | Description |
|:-----------|:------------|
| **Mobile App** | Flutter-based driver monitoring application with real-time camera integration |
| **Web Dashboard** | React-based admin portal for fleet management and analytics |
| **Backend API** | .NET RESTful API for authentication, trip management, and data services |
| **AI Models** | P-YOLOv8 and DMD-based deep learning models for detection |

<br>

## Team

<table>
<tr>
<th width="28%">Member</th>
<th width="22%">Role</th>
<th width="50%">Responsibilities</th>
</tr>
<tr>
<td><strong>Haneen Hassan El-Sayed</strong></td>
<td>Mobile Developer</td>
<td>Flutter app — UI/UX design, camera integration, real-time alerts, cross-platform performance</td>
</tr>
<tr>
<td><strong>Abdulrahman Ehab Taha</strong></td>
<td>Front-End Developer</td>
<td>React dashboard — responsive design, data visualization, fleet management interface</td>
</tr>
<tr>
<td><strong>Shehab Mohamed Kamal</strong></td>
<td>Back-End Developer</td>
<td>.NET API — server-side logic, database management, system integration</td>
</tr>
<tr>
<td><strong>Omar Khalid Saber</strong></td>
<td>Back-End Developer</td>
<td>.NET API — API development, performance optimization, secure data communication</td>
</tr>
<tr>
<td><strong>Abdulrahman Eldeeb</strong></td>
<td>AI Developer</td>
<td>Deep learning — model architecture design, training, and deployment</td>
</tr>
<tr>
<td><strong>Shehab Yasser Ali</strong></td>
<td>AI Developer</td>
<td>Deep learning — data preprocessing, model evaluation, inference optimization</td>
</tr>
</table>

<br>

<div align="center">

### Supervisors

**Dr. Mary Monir** · **Eng. Malak Ahmed** · **Eng. Khaled Ahmed**

<br>

Faculty of Computers and Artificial Intelligence

Graduation Project — 2025 / 2026

<br>

---

<br>

*Ala Mahlak — Because every driver deserves to arrive safely.*

<br>

</div>
