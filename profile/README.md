<div align="center">

# Ala Mahlak

### AI-Powered Driver Monitoring System

> Reducing road accidents through real-time drowsiness and distraction detection using deep learning and computer vision.

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=csharp&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)

</div>

---

## About

**Ala Mahlak** (Arabic: على مهلك — "Take it easy") is an AI-powered driver monitoring system designed to tackle the rising threat of accidents caused by distracted and drowsy driving. The system combines a **mobile application** for real-time detection and alerting with a **web portal** for fleet management, analytics, and reporting.

Unlike traditional DMS solutions that depend on expensive infrared cameras and proprietary vehicle hardware, Ala Mahlak takes a **software-first approach** — running entirely on standard smartphone cameras. This makes it accessible, affordable, and deployable at scale, especially in developing markets like the MENA region where existing solutions have limited reach.

---

## The Problem

<table>
<tr>
<td width="50%">

### Why This Matters

- **42,915** fatalities from motor vehicle crashes in 2021 (NHTSA) — the highest since 2005
- **10.5%** single-year increase — the largest jump in FARS history
- Drowsy driving reduces reaction time, decision-making ability, and situation awareness
- Drivers often **misjudge** their own drowsiness and distraction levels
- Existing DMS solutions are **expensive**, **hardware-dependent**, and **inaccessible** in developing markets

</td>
<td width="50%">

### Gaps in Current Industry Solutions

- **High cost** — Specialized IR sensors, edge-AI processors, and vehicle integration
- **Hardware-locked** — Difficult to upgrade older vehicles or deploy across diverse fleets
- **No local customization** — Models trained in Europe/US/Japan fail on MENA conditions (harsh sun, diverse facial features, cultural clothing)
- **Reactive, not predictive** — Current systems detect fatigue but can't anticipate it
- **Privacy concerns** — Continuous face recording raises GDPR and ethical issues

</td>
</tr>
</table>

---

## How It Works

```
┌─────────────────┐     Camera Feed      ┌─────────────────┐     Detection Results     ┌─────────────────┐
│                 │ ──────────────────── > │                 │ ──────────────────────── > │                 │
│   Mobile App    │                       │    AI Server     │                           │  Alert System   │
│   (Flutter)     │ < ──────────────────── │   (Python/DL)   │                           │  (Audio/Visual) │
│                 │    Real-time Alerts    │                 │                           │                 │
└────────┬────────┘                       └────────┬────────┘                           └─────────────────┘
         │                                         │
         │  Trip Data & Reports                    │  Analytics & Insights
         │                                         │
         v                                         v
┌─────────────────┐                       ┌─────────────────┐
│                 │                       │                 │
│   Backend API   │ < ─────────────────── │  Web Dashboard  │
│   (.NET / C#)   │ ──────────────────── >│    (React)      │
│                 │    Fleet Management   │                 │
└─────────────────┘                       └─────────────────┘
```

1. **Capture** — The mobile app accesses the smartphone's front camera to stream real-time video of the driver.
2. **Analyze** — Frames are sent to the AI server, where deep learning models detect drowsiness (eye closure, yawning) and distraction (phone usage, looking away, inattention).
3. **Alert** — When unsafe behavior is detected, the driver receives **instant visual and audio alerts** within 1 second.
4. **Report** — Trip data, detection events, and performance metrics are stored and made available through the web dashboard for fleet managers and admins.

---

## System Architecture

| Layer | Technology | Purpose |
|:------|:-----------|:--------|
| **Mobile Application** | Flutter, Dart | Cross-platform app for real-time camera capture, driver alerts, trip management, and company onboarding |
| **Web Dashboard** | React, JavaScript | Admin portal for fleet monitoring, driver analytics, trip review, safety reports, and company management |
| **Backend API** | .NET 8, C#, ASP.NET | RESTful API with server-side logic, authentication, role management, database operations, and secure communication |
| **AI / Deep Learning** | Python, PyTorch, TensorFlow/Keras, OpenCV | CNN-based models for drowsiness and distraction detection — MTCNN, MobileNetV3, P-YOLOv8, EfficientNet |
| **Database** | SQL Server | Relational storage for users, companies, trips, reports, and aggregate analytics |
| **Training Environment** | Google Colab (GPU/TPU) | Cloud-based training and experimentation for deep learning models |

---

## AI Models & Detection

The system uses a multi-model pipeline combining state-of-the-art deep learning architectures:

| Model | Task | Key Details |
|:------|:-----|:------------|
| **MTCNN** | Face Detection & Alignment | Multi-stage cascaded CNN for precise facial localization, robust against partial occlusions |
| **MobileNetV3-Small** | Occlusion Detection | Lightweight architecture optimized for on-device inference; depthwise separable convolutions |
| **P-YOLOv8** | Distraction Classification | Pruned YOLOv8 — only **2.84 MB**, ~**1.45M** parameters, **99.46%** accuracy, **12.9ms** inference |
| **EfficientNetB0 + Channel Attention** | Distraction Detection | **99.58%** accuracy at **83.75 FPS**, only **5 MB** model size |
| **YOLOv5/v8 + SVM** | Drowsiness Detection | **99.5% mAP**, **99.9%** precision for yawning and eye closure detection |

### Datasets Used

| Dataset | Type | Use Case |
|:--------|:-----|:---------|
| **DMD** (Driving Monitoring Dataset) | RGB + IR, multimodal | Gaze estimation, occlusion detection, drowsiness |
| **State Farm** Distracted Driver Detection | RGB, 10 distraction classes | Distraction classification (texting, eating, phone, etc.) |
| **AUCD2** (AUC Distracted Driver) | RGB, balanced classes | Distracted driving behavior detection |
| **NTHU-DDD** | Video, drowsiness levels | Drowsiness detection (microsleep, yawning) |
| **UTA-RLDD** | Video, 3 vigilance states | Real-life drowsiness with diverse demographics |

---

## Key Features

<table>
<tr>
<td width="50%">

### For Drivers (Mobile App)

- Real-time drowsiness and distraction detection
- Instant visual and audio alerts
- Trip start/end with automatic monitoring
- Trip history and past ride review
- Request to join a company fleet
- Accept company invitations
- In-app chat with fleet admins
- Profile management and password recovery

</td>
<td width="50%">

### For Fleet Managers (Web Dashboard)

- Enterprise dashboard with safety analytics
- Monitor all company drivers and their trips
- Review individual trip reports with detection events
- Approve/reject driver join requests
- Send invitations to drivers
- Add or remove drivers from company fleet
- Create and manage admin accounts
- Role-based access control (Driver, Admin, Company)

</td>
</tr>
</table>

---

## Performance Targets

| Metric | Target |
|:-------|:-------|
| Detection latency | **< 500 ms** per camera frame |
| Alert response time | **< 1 second** from detection |
| AI detection accuracy | **>= 95%** for drowsiness and distraction |
| Mobile resource usage | **<= 20% CPU**, **<= 200 MB RAM** |
| Dashboard load time | **< 3 seconds** for up to 100 concurrent users |
| Scalability | Up to **10,000** enterprise users and **100,000** drivers |
| Data security | **TLS/AES** encryption, **GDPR**-compliant |

---

## Project Timeline

```
Sep 2025                                                                          May 2026
  │                                                                                  │
  ├──── Phase 1 ────┤                                                                │
  │  Planning &      ├──── Phase 2 ─────────┤                                        │
  │  Requirements    │  System Design        ├──── Phase 3 ──────────────┤            │
  │                  │                       │  Backend Development      │            │
  │                  ├──── Phase 4 ──────────────────────────────────────────────┤    │
  │                  │  AI Model Development & Training                  │       │    │
  │                  │                                    ├──── Phase 5 ─┤       │    │
  │                  │                                    │  Mobile & Web│       │    │
  │                  │                                    │  Development ├── Phase 6 ─┤
  │                  │                                    │              │  Integration│
  │                  │                                    │              │  & Testing  ├─ Phase 7
  │                  │                                    │              │             │ Deployment
  │                                                                                  │
  Sep               Oct              Dec              Feb             Apr            May
```

**Total Duration:** 9.75 months (September 2025 – May 2026)

---

## Repositories

| Repository | Description |
|:-----------|:------------|
| **Mobile App** | Flutter-based driver monitoring application with real-time camera integration |
| **Web Dashboard** | React-based admin portal for fleet management and analytics |
| **Backend API** | .NET RESTful API for authentication, trip management, and data services |
| **AI Models** | Deep learning models for drowsiness and distraction detection |

---

## Tech Stack at a Glance

<table>
<tr>
<th>Category</th>
<th>Technologies</th>
</tr>
<tr>
<td><strong>Mobile</strong></td>
<td>Flutter, Dart</td>
</tr>
<tr>
<td><strong>Web Frontend</strong></td>
<td>React, JavaScript</td>
</tr>
<tr>
<td><strong>Backend</strong></td>
<td>.NET, C#, ASP.NET, Entity Framework</td>
</tr>
<tr>
<td><strong>AI/ML</strong></td>
<td>Python, PyTorch, TensorFlow, Keras, OpenCV, NumPy, Pandas</td>
</tr>
<tr>
<td><strong>Models</strong></td>
<td>MTCNN, MobileNetV3, P-YOLOv8, EfficientNetB0, YOLOv5/v8, SVM</td>
</tr>
<tr>
<td><strong>Database</strong></td>
<td>SQL Server</td>
</tr>
<tr>
<td><strong>Visualization</strong></td>
<td>Matplotlib, Seaborn</td>
</tr>
<tr>
<td><strong>Training</strong></td>
<td>Google Colab (GPU/TPU)</td>
</tr>
</table>

---

## Team

<table>
<tr>
<th>Member</th>
<th>Role</th>
<th>Focus Area</th>
</tr>
<tr>
<td><strong>Haneen Hassan El-Sayed</strong></td>
<td>Mobile Developer</td>
<td>Flutter app — UI/UX, camera integration, real-time alerts, cross-platform performance</td>
</tr>
<tr>
<td><strong>Abdulrahman Ehab Taha</strong></td>
<td>Front-End Developer</td>
<td>React dashboard — responsive design, data visualization, fleet management interface</td>
</tr>
<tr>
<td><strong>Shehab Mohamed Kamal</strong></td>
<td>Back-End Developer</td>
<td>.NET API — server-side logic, database management, mobile/web integration</td>
</tr>
<tr>
<td><strong>Omar Khalid Saber</strong></td>
<td>Back-End Developer</td>
<td>.NET API — API development, performance optimization, secure data communication</td>
</tr>
<tr>
<td><strong>Abdulrahman Eldeeb</strong></td>
<td>AI Developer</td>
<td>Deep learning — model design, training, and deployment for drowsiness/distraction detection</td>
</tr>
<tr>
<td><strong>Shehab Yasser Ali</strong></td>
<td>AI Developer</td>
<td>Deep learning — data preprocessing, model evaluation, real-time inference optimization</td>
</tr>
</table>

### Supervisors

| Supervisor | Role |
|:-----------|:-----|
| **Dr. Mary Monir** | Project Supervisor |
| **Eng. Malak Ahmed** | Teaching Assistant |
| **Eng. Khaled Ahmed** | Teaching Assistant |

<div align="center">

**Faculty of Computers and Artificial Intelligence**

Graduation Project 2025 — 2026

---

*Ala Mahlak — Because every driver deserves to arrive safely.*

</div>
