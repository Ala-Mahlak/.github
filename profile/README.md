<div align="center">

<img src="https://ala-mahlak.runasp.net/images/logo/Ala-Mahlak-Logo.png" alt="Ala Mahlak logo" width="220" />

# Ala Mahlak

#### على مهلك

**Real-time AI-powered driver monitoring for safer trips and smarter fleet operations.**

[![Flutter](https://img.shields.io/badge/Flutter-Mobile-02569B?style=flat-square&logo=flutter&logoColor=white)](https://github.com/Ala-Mahlak/Ala-Mahlak-Flutter)
[![React](https://img.shields.io/badge/React-Dashboard-20232A?style=flat-square&logo=react&logoColor=61DAFB)](https://github.com/Ala-Mahlak/Ala-Mahlak-Frontend)
[![.NET](https://img.shields.io/badge/.NET-Backend-512BD4?style=flat-square&logo=dotnet&logoColor=white)](https://github.com/Ala-Mahlak/Ala-Mahlak-Backend)
[![Django](https://img.shields.io/badge/Django-AI_API-092E20?style=flat-square&logo=django&logoColor=white)](https://github.com/Ala-Mahlak/Ala-Mahlak-AI)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer_Vision-5C3EE8?style=flat-square&logo=opencv&logoColor=white)](https://github.com/Ala-Mahlak/Ala-Mahlak-AI)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Object_Detection-111827?style=flat-square)](https://github.com/Ala-Mahlak/Ala-Mahlak-AI)

[Overview](#overview) • [Architecture](#architecture) • [Repositories](#repositories) • [Features](#features) • [Tech Stack](#tech-stack) • [Getting Started](#getting-started) • [Project Context](#project-context)

</div>

---

## Overview

**Ala Mahlak** is a multi-repository driver-safety platform designed around camera-based driver monitoring, trip management, company administration, and fleet visibility.

The project brings together four main components:

| Component | Audience | Primary responsibility |
| --- | --- | --- |
| Mobile app | Drivers | Ride planning, trip lifecycle, camera-based monitoring, trip history, profile workflows |
| Web dashboard | Companies and admins | Fleet overview, driver management, trip monitoring, alerts, support, company profile workflows |
| Backend API | Apps and services | Authentication, companies, users, trips, chat, reports, static files, shared contracts |
| AI service | Mobile/backend clients | Image-based drowsiness and distraction analysis with computer vision |

> [!NOTE]
> This repository is the GitHub organization profile. Runtime instructions, API details, and implementation notes live in the component repositories linked below.

## Why Ala Mahlak Exists

Road safety depends on human attention, but fatigue and distraction are difficult to detect from trip records alone. Ala Mahlak approaches the problem as a connected software system rather than a single isolated model.

The system combines:

| Need | Ala Mahlak approach |
| --- | --- |
| Driver-facing monitoring | A Flutter mobile app with camera, location, trip, map, and profile flows |
| AI-based driver analysis | A Django REST Framework service using facial landmarks, head pose, drowsiness scoring, YOLOv8 object detection, and signal fusion |
| Fleet administration | A React/Vite dashboard for companies, admins, drivers, trips, alerts, support, and reporting |
| Application backend | An ASP.NET Core API with JWT auth, role-based access, company workflows, trip lifecycle, reports, and SignalR chat |

The name **Ala Mahlak** means **"take it easy"** or **"slow down"**, which matches the project goal: give drivers and fleet operators better visibility before unsafe driving becomes an incident.

## Architecture

```text
                                      +-----------------------------+
                                      |        AI Service            |
                                      |  Django REST Framework       |
                                      |  MediaPipe + OpenCV + YOLOv8 |
                                      +--------------+--------------+
                                                     ^
                                                     |
                         uploaded frame / image      | analysis result
                                                     |
+-----------------------------+          +-----------+-------------+          +-----------------------------+
|        Mobile App           |          |       Backend API       |          |       Web Dashboard         |
|  Flutter                    |          |  ASP.NET Core           |          |  React + TypeScript + Vite  |
|  Camera, rides, maps, auth  +--------->|  Auth, companies, trips +<---------+  Fleet, drivers, alerts     |
|  profile, trip history      |          |  chat, reports, files   |          |  support, profiles          |
+-----------------------------+          +-----------+-------------+          +-----------------------------+
                                                     |
                                                     v
                                      +-----------------------------+
                                      |       SQL Server            |
                                      |  Users, companies, trips,   |
                                      |  chat, reports, relations   |
                                      +-----------------------------+
```

## Main Data Flows

| Flow | Source | Destination | What happens |
| --- | --- | --- | --- |
| Authentication | Mobile app / web dashboard | Backend API | Users and companies register, verify email, log in, refresh sessions, and update profiles |
| Company membership | Mobile app / web dashboard | Backend API | Drivers search companies, submit join requests, and admins approve or reject membership |
| Trip lifecycle | Mobile app | Backend API | Drivers start trips, end trips, update highest speed, and review trip history |
| Driver monitoring | Mobile app camera | AI service | Captured frames are analyzed for drowsiness and distraction signals |
| Fleet monitoring | Web dashboard | Backend API | Company/admin users review drivers, trips, reports, and alert-oriented screens |
| Support and chat | Mobile/web clients | Backend API + SignalR | Users and admins exchange messages through REST endpoints and realtime hub support |
| Reporting | Web dashboard | Backend API | Company/admin users can request PDF driver reports |

## Repositories

<table>
<tr>
<th width="24%">Repository</th>
<th width="20%">Layer</th>
<th width="56%">What it contains</th>
</tr>
<tr>
<td><a href="https://github.com/Ala-Mahlak/Ala-Mahlak-Flutter"><strong>Ala-Mahlak-Flutter</strong></a></td>
<td>Mobile app</td>
<td>Flutter application under <code>gradprojct/</code> with auth, onboarding, map/routing flows, camera-based ride monitoring, trip history, chat/profile screens, and Android/iOS projects.</td>
</tr>
<tr>
<td><a href="https://github.com/Ala-Mahlak/Ala-Mahlak-Frontend"><strong>Ala-Mahlak-Frontend</strong></a></td>
<td>Web dashboard</td>
<td>React 19 + TypeScript + Vite dashboard with company auth, dashboards, drivers, companies, trip monitoring, alerts, assignment, support, and profile pages.</td>
</tr>
<tr>
<td><a href="https://github.com/Ala-Mahlak/Ala-Mahlak-Backend"><strong>Ala-Mahlak-Backend</strong></a></td>
<td>Backend API</td>
<td>ASP.NET Core solution with API, Core, Infrastructure, Service, and Shared projects for auth, companies, trips, chat, reports, JWT, EF Core, SQL Server, and SignalR.</td>
</tr>
<tr>
<td><a href="https://github.com/Ala-Mahlak/Ala-Mahlak-AI"><strong>Ala-Mahlak-AI</strong></a></td>
<td>AI service</td>
<td>Django REST Framework API for driver-image analysis using MediaPipe FaceMesh, OpenCV head-pose estimation, drowsiness scoring, YOLOv8 object detection, preprocessing, and fusion logic.</td>
</tr>
</table>

## Repository Map

```text
Ala-Mahlak/
|-- .github/
|   `-- profile/README.md                # Organization profile shown on GitHub
|-- Ala-Mahlak-Flutter/
|   `-- gradprojct/                      # Flutter mobile application
|-- Ala-Mahlak-Frontend/                 # React/Vite company dashboard
|-- Ala-Mahlak-Backend/                  # ASP.NET Core backend solution
`-- Ala-Mahlak-AI/                       # Django computer-vision API
```

## Features

### Platform Capabilities

| Capability | Mobile app | Web dashboard | Backend API | AI service |
| --- | --- | --- | --- | --- |
| Driver registration/login | Yes | No | Yes | No |
| Company registration/login | No | Yes | Yes | No |
| Email verification/password reset | Yes | Yes | Yes | No |
| Company search and join requests | Yes | Yes | Yes | No |
| Driver and admin management | No | Yes | Yes | No |
| Trip start/end/history | Yes | Yes | Yes | No |
| Highest-speed update | Yes | No | Yes | No |
| Driver monitoring frames | Yes | No | No | Yes |
| Drowsiness analysis | No | No | No | Yes |
| Distraction analysis | No | No | No | Yes |
| Chat and support flows | Yes | Yes | Yes | No |
| PDF driver reports | No | Yes | Yes | No |
| Swagger/OpenAPI documentation | No | No | Yes | Yes |

### Driver Experience

The Flutter app is the driver-facing entry point. Evidence in the mobile repository shows support for:

| Area | Details |
| --- | --- |
| Authentication | Registration, login, email verification, profile completion, token persistence |
| Navigation | `go_router` routing and a main app shell with Home, Search, New Ride, Chat, and Profile tabs |
| Maps and routing | LocationIQ search, reverse geocoding, map tiles, current location, route distance calculation |
| Trips | Ride start/end API calls and previous trip history display |
| Monitoring | Front-camera capture that periodically uploads frames to a distraction-analysis endpoint |
| Device features | Camera, image picker, location permissions, Android and iOS platform projects |

### Fleet And Admin Experience

The web dashboard is the company/admin-facing interface. Evidence in the frontend repository shows support for:

| Area | Details |
| --- | --- |
| Authentication | Company login, registration, forgot-password, OTP reset, protected routes |
| Dashboard | Fleet KPIs, recent distraction alerts, active driver summaries |
| Companies | Admin list, create/promote/downgrade/remove admins, company reports |
| Drivers | API-backed company driver lists, search, filters, detail pages |
| Trips | Company trips and trip monitoring views |
| Alerts | Phone usage, drowsiness, looking away, eating/drinking review screens backed by local mock data |
| Assignment | Company-code sharing and pending join-request decisions |
| Support | Mock live chat and tickets through React Query cache updates |
| Profile | Local profile edits and API-backed company logo upload/removal |

> [!NOTE]
> The frontend currently mixes API-backed screens with mock data from `src/data/mockData.ts`. The component README identifies which areas are mocked and which call the backend.

### Backend Capabilities

The backend is an ASP.NET Core API organized as a multi-project solution:

| Project | Responsibility |
| --- | --- |
| `AlaMahlak.API` | ASP.NET Core host, controllers, SignalR hub, static files, Swagger |
| `AlaMahlak.Core` | Domain entities, EF Core entity configurations, repository interfaces |
| `AlaMahlak.Infrastructure` | EF Core `DbContext`, generic repository, unit of work |
| `AlaMahlak.Service` | Application services for auth, companies, trips, chat, and email |
| `AlaMahlak.Shared` | Request/response contracts, settings models, error responses, error codes |

Key backend areas include:

| Area | Evidence-backed functionality |
| --- | --- |
| Auth | Register, login, logout, email verification, profile update, password reset |
| Companies | Company registration/login, lookup, join requests, members, admins, logos, reports |
| Trips | Current-user trips, start trip, end active trip, update highest speed |
| Chat | Contacts, conversations, messages, SignalR broadcasts |
| Files | Static file serving for uploaded profile/company images and logo assets |
| Reports | PDF driver report generation through QuestPDF |

### AI And Computer Vision

The AI service analyzes uploaded driver images and returns structured drowsiness/distraction results.

| Pipeline stage | Implementation evidence |
| --- | --- |
| API layer | Django 4.2, Django REST Framework, multipart uploads, `drf-spectacular` docs |
| Image validation | JPEG, JPG, PNG, BMP, WebP support with upload-size checks |
| Preprocessing | CLAHE, dynamic gamma correction, gray-world white balance, conditional denoising |
| Face landmarks | MediaPipe FaceMesh landmark extraction |
| Eye/mouth metrics | EAR and MAR calculations for drowsiness/yawning signals |
| Head pose | OpenCV `solvePnP` pitch, yaw, roll estimation |
| Gaze | Horizontal and vertical gaze estimation |
| Object detection | Ultralytics YOLOv8 for COCO phone, drink, and food-related classes |
| Fusion | Rule-based signal fusion into safe/drowsy/distracted classes |
| Tests | `pytest` and `pytest-django` coverage for API, drowsiness, FaceMesh, fusion, pose, and YOLO degraded mode |

> [!IMPORTANT]
> The AI REST API analyzes one uploaded image per request. Temporal behavior such as PERCLOS, blink rate, state debounce, and camera-offset calibration is implemented in the webcam demo rather than the stateless REST endpoint.

## Tech Stack

### Technology Matrix

| Layer | Main technologies | Supporting packages/tools |
| --- | --- | --- |
| Mobile | Flutter, Dart | `go_router`, `flutter_bloc`, `dio`, `http`, `camera`, `image_picker`, `shared_preferences`, `geolocator`, `flutter_map`, LocationIQ |
| Web | React 19, TypeScript, Vite | Tailwind CSS 4, Material UI, TanStack Query, React Router, Framer Motion, Lucide React, ESLint |
| Backend | .NET 10, ASP.NET Core, C# | EF Core 10, SQL Server, JWT Bearer auth, SignalR, MailKit, MimeKit, BCrypt.Net, QuestPDF, Swashbuckle |
| AI service | Python, Django 4.2, Django REST Framework | MediaPipe, OpenCV, NumPy, Pydantic v2, Ultralytics YOLOv8, drf-spectacular, Gunicorn, WhiteNoise |
| Testing | pytest, pytest-django, Flutter test dependencies, ESLint | Backend currently documents build verification rather than a checked-in test project |
| Deployment evidence | Azure Container Apps workflow for AI, live hosted backend Swagger | Dockerfile for AI service, Gunicorn, Azure Container Registry workflow |

### Runtime And Tooling Snapshot

| Repository | Runtime/tooling evidence |
| --- | --- |
| `Ala-Mahlak-Flutter` | Dart SDK constraint `^3.10.8`, Android/iOS projects, `flutter_lints`, `flutter_launcher_icons` |
| `Ala-Mahlak-Frontend` | Vite 6, TypeScript 5.8, React 19, ESLint 9, Tailwind CSS 4 |
| `Ala-Mahlak-Backend` | Target framework `net10.0`, SQL Server through EF Core, Swagger enabled |
| `Ala-Mahlak-AI` | Python 3.11 Docker image, Django 4.2, DRF, OpenCV/MediaPipe runtime dependencies |

## API Surface

### Backend API Summary

The backend README documents these endpoint groups:

| Group | Example endpoints | Purpose |
| --- | --- | --- |
| Auth | `POST /api/auth/register`, `POST /api/auth/login`, `GET /api/auth/me` | User/company registration, login, profile, verification, password reset |
| Companies | `GET /api/companies`, `POST /api/companies/join-requests`, `PUT /api/companies/logo` | Company lookup, membership, admins, drivers, logo, reports |
| Trips | `GET /api/trips/me`, `POST /api/trips/start`, `POST /api/trips/end` | User trip lifecycle and highest-speed tracking |
| Chat | `GET /api/chat/contacts`, `POST /api/chat/messages` | Contacts, conversations, messages |
| Realtime | `/hubs/chat` | SignalR chat hub with JWT support through `access_token` query string |
| Health | `GET /api/health` | Public backend health check |

Live backend Swagger documentation is available at:

```text
https://ala-mahlak.runasp.net/swagger/index.html
```

### AI Service API Summary

| Method | Path | Description |
| --- | --- | --- |
| `GET` | `/` | Redirects to `/api/docs` |
| `GET` | `/api/docs` | Swagger UI |
| `GET` | `/api/schema` | OpenAPI schema generated by `drf-spectacular` |
| `GET` | `/api/v1/health` | Health check with service version and YOLO status |
| `POST` | `/api/v1/analyze` | Full driver image analysis response |
| `POST` | `/api/v1/analyze/simple` | Compact analysis response for lightweight clients |

Example AI request:

```bash
curl -X POST "http://localhost:8000/api/v1/analyze" \
  -H "accept: application/json" \
  -F "file=@driver_photo.jpg"
```

The full AI response includes driver state, distraction status, drowsiness score, raw EAR/MAR/head-pose metrics, detected objects, status, timing, explanation, and optional errors.

## Getting Started

This organization contains separate applications. Choose the component you want to run first.

### Run The Mobile App

```bash
git clone https://github.com/Ala-Mahlak/Ala-Mahlak-Flutter.git
cd Ala-Mahlak-Flutter/gradprojct
flutter pub get
flutter run
```

> [!WARNING]
> The Flutter app currently stores service URLs, a LocationIQ key, and a distraction-analysis CSRF token directly in source files. Rotate exposed credentials if needed and move production secrets out of the app before release.

### Run The Web Dashboard

```bash
git clone https://github.com/Ala-Mahlak/Ala-Mahlak-Frontend.git
cd Ala-Mahlak-Frontend
npm install
npm run dev
```

The Vite dev server proxies `/api/*` requests to the hosted backend URL configured in `vite.config.ts`.

### Run The Backend API

```bash
git clone https://github.com/Ala-Mahlak/Ala-Mahlak-Backend.git
cd Ala-Mahlak-Backend
dotnet restore AlaMahlak.sln
dotnet run --project AlaMahlak.API
```

The backend repository does not include `appsettings*.json`. Provide configuration through user secrets, environment variables, or another ASP.NET Core configuration provider.

Minimum configuration areas:

| Area | Example setting |
| --- | --- |
| SQL Server | `ConnectionStrings__DefaultConnection` |
| JWT | `JwtOptions__SecretKey`, `JwtOptions__Issuer`, `JwtOptions__Audience` |
| SMTP | `SmtpSettings__Host`, `SmtpSettings__Username`, `SmtpSettings__Password` |
| App URL | `AppSettings__ApiBaseUrl` |

### Run The AI Service

```bash
git clone https://github.com/Ala-Mahlak/Ala-Mahlak-AI.git
cd Ala-Mahlak-AI
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
cp .env.example .env
python manage.py migrate
python manage.py runserver 0.0.0.0:8000
```

Open the local AI docs at:

```text
http://localhost:8000/api/docs
```

## Configuration Notes

| Repository | Configuration model |
| --- | --- |
| Mobile | Service endpoints and API keys are currently hard-coded in Dart source files |
| Frontend | API requests use `BASE_URL = '/api'`; dev proxy targets the hosted backend |
| Backend | ASP.NET Core configuration sections for connection strings, JWT, SMTP, and app settings |
| AI | `.env.example` and `.env.azure.example` cover Django, CORS/CSRF, YOLO, upload size, and Azure settings |

## Deployment Notes

| Repository | Evidence-backed deployment state |
| --- | --- |
| Mobile | Android and iOS platform projects are present; build commands are documented in the component README |
| Frontend | Vite production build is available through `npm run build`; production must serve or proxy `/api` correctly |
| Backend | Live Swagger is available; no Docker or deployment manifests are checked in |
| AI | Dockerfile and GitHub Actions workflow exist for Azure Container Registry and Azure Container Apps deployment |

AI container summary:

| Detail | Value |
| --- | --- |
| Base image | `python:3.11-slim` |
| Server | Gunicorn with `dms.wsgi:application` |
| Port | `8000` |
| Health check | `/api/v1/health` |
| Production dependencies | `requirements-azure.txt`, `opencv-python-headless`, Gunicorn, WhiteNoise |

## Quality And Verification

| Repository | Current verification path |
| --- | --- |
| Mobile | `flutter analyze`, `flutter test`, `flutter build apk`, `flutter build ios` are documented; existing widget test is still the default counter test |
| Frontend | `npm run build`, `npm run lint`, `npm run preview`; no test script is configured |
| Backend | `dotnet build AlaMahlak.sln`; no checked-in test project is present |
| AI | `pytest tests/ -v` covers API behavior, drowsiness, FaceMesh, fusion, pose estimation, and YOLO degraded mode |

> [!TIP]
> For the fastest end-to-end orientation, read the component READMEs in this order: backend, AI service, mobile app, frontend dashboard. That order explains the APIs before the clients that consume them.

## Security And Privacy Notes

| Topic | Current repository evidence |
| --- | --- |
| Authentication | Backend uses JWT bearer authentication and role-based authorization |
| Password handling | Backend uses BCrypt.Net for password hashing |
| Email workflows | Backend uses SMTP settings with MailKit/MimeKit for verification and password reset |
| Secrets | Backend and AI document environment/configuration values; Flutter currently includes hard-coded service configuration |
| File uploads | Backend serves uploaded profile/company images; AI validates image type and upload size |
| CORS/CSRF | AI service exposes CORS and CSRF environment variables |
| Production caution | Do not commit real database strings, JWT signing keys, SMTP credentials, API keys, or service tokens |

## Project Structure By Layer

### Mobile App

```text
Ala-Mahlak-Flutter/
`-- gradprojct/
    |-- android/              # Android platform project and permissions
    |-- animation/            # Lottie animation assets
    |-- images/               # Logo, onboarding, auth, map, chat, profile, UI assets
    |-- ios/                  # iOS platform project and permission descriptions
    |-- lib/
    |   |-- core/             # API clients, routing, local storage, services, themes
    |   `-- features/         # Auth, intro, splash, main tabs, map, rides, chat, profile
    |-- test/                 # Flutter widget tests
    `-- pubspec.yaml          # Dependencies, assets, launcher icon config
```

### Web Dashboard

```text
Ala-Mahlak-Frontend/
|-- src/
|   |-- assets/               # Logo animations and local SVG assets
|   |-- components/           # Shared app shell components
|   |-- context/              # Auth context and session state
|   |-- data/                 # Mock dashboard, alert, trip, support, driver data
|   |-- hooks/                # React Query data hooks
|   |-- pages/                # Route-level pages
|   `-- services/             # Backend API client and session helpers
|-- package.json              # Scripts and dependencies
`-- vite.config.ts            # Vite plugins and dev API proxy
```

### Backend API

```text
Ala-Mahlak-Backend/
|-- AlaMahlak.sln
|-- AlaMahlak.API/            # ASP.NET Core host, controllers, SignalR hub, static files
|-- AlaMahlak.Core/           # Domain entities, EF Core configs, repository interfaces
|-- AlaMahlak.Infrastructure/ # EF Core DbContext, repositories, unit of work
|-- AlaMahlak.Service/        # Auth, companies, trips, chat, email services
`-- AlaMahlak.Shared/         # Contracts, settings models, error responses/codes
```

### AI Service

```text
Ala-Mahlak-AI/
|-- api/
|   |-- core/                 # MediaPipe singleton, YOLO wrapper, fusion engine
|   |-- schemas/              # Pydantic response models and enums
|   |-- services/             # DriverMonitorService orchestration pipeline
|   |-- utils/                # Image decoding, validation, conversion
|   |-- vision/               # FaceMesh, head pose, drowsiness analysis
|   |-- config.py             # Thresholds, model paths, runtime settings
|   `-- views.py              # Health and analyze views
|-- dms/                      # Django settings, URLs, ASGI, WSGI
|-- tests/                    # pytest and pytest-django tests
|-- Dockerfile
|-- openapi.yaml
|-- requirements.txt
`-- webcam_demo.py
```

## User Journeys

### Driver Journey

| Step | System behavior |
| --- | --- |
| 1 | Driver creates an account or logs in from the Flutter app |
| 2 | Driver completes profile and stores session tokens locally |
| 3 | Driver searches/selects route information through map and LocationIQ flows |
| 4 | Driver starts a trip through the backend API |
| 5 | Mobile app uses front-camera monitoring during the ride |
| 6 | Captured frames are sent to the AI analysis endpoint |
| 7 | Trip can be ended and previous trip details can be reviewed |

### Company/Admin Journey

| Step | System behavior |
| --- | --- |
| 1 | Company user registers/logs in from the web dashboard |
| 2 | Company reviews dashboard KPIs and active driver summaries |
| 3 | Company handles pending driver join requests |
| 4 | Company manages admins and drivers through backend API-backed pages |
| 5 | Company reviews trips, alerts, reports, and profile/logo settings |
| 6 | Company/admin uses support and chat workflows where implemented |

### AI Analysis Journey

| Step | System behavior |
| --- | --- |
| 1 | Client uploads a driver image as multipart form data |
| 2 | API validates content type, file presence, and upload size |
| 3 | Image is decoded and preprocessed for lighting and noise conditions |
| 4 | FaceMesh extracts landmarks for eyes, mouth, gaze, and head pose inputs |
| 5 | YOLOv8 detects relevant objects such as phone, drink, and food classes |
| 6 | Drowsiness and distraction signals are fused into a driver state |
| 7 | API returns structured JSON with confidence, explanation, metrics, and status |

## Current Gaps And Known Risks

| Area | Current state |
| --- | --- |
| Mobile secrets | Some service URLs, keys, and tokens are committed in Flutter source files |
| Frontend tests | No test script is configured in `package.json` |
| Frontend mock data | Several dashboard/support/alert areas use local mock data |
| Backend configuration | `appsettings*.json` is not checked in, so setup requires external configuration |
| Backend migrations/tests | No EF migrations or test projects are currently present in the backend solution |
| AI API temporal context | REST endpoint is stateless; temporal logic is in `webcam_demo.py` |
| AI OpenAPI snapshot | Checked-in OpenAPI and live Django routes should be kept in sync as endpoints evolve |

## Project Context

This organization represents a graduation-project style platform built around a practical road-safety idea: use widely available software and smartphone capabilities to make driver monitoring more accessible.

Academic project metadata preserved from the original organization profile:

| Item | Details |
| --- | --- |
| Project | Ala Mahlak - real-time AI-powered driver monitoring system |
| Institution context | Faculty of Computers and Artificial Intelligence |
| Academic year | 2025 / 2026 |
| Timeline | September 2025 to May 2026 |
| Core disciplines | Mobile development, frontend development, backend development, AI/computer vision |

## Project Timeline

```text
Sep 2025                                                        May 2026
   |                                                              |
   |  Planning      Design        Backend       Integration       |
   |  and           and           and API       and testing        |
   |  requirements  architecture  development   across apps        |
   |      |            |              |              |             |
   +------+------------+--------------+--------------+-------------+
          |                           |
          |                           +-- Mobile and web development
          |
          +-- AI model, preprocessing, detection, and API work
```

## Team

| Member | Role | Focus area |
| --- | --- | --- |
| Haneen Hassan El-Sayed | Mobile Developer | Flutter app, UI/UX, camera integration, cross-platform flows |
| Abdulrahman Ehab Taha | Frontend Developer | React dashboard, responsive interface, dashboard workflows |
| Shehab Mohamed Kamal | Backend Developer | .NET API, server-side logic, database integration |
| Omar Khalid Saber | Backend Developer | API development, performance, secure communication |
| Abdulrahman Eldeeb | AI Developer | Model architecture, training, deployment-oriented AI work |
| Shehab Yasser Ali | AI Developer | Data preprocessing, model evaluation, inference optimization |

Supervisors:

| Supervisor |
| --- |
| Dr. Mary Monir |
| Eng. Malak Ahmed |
| Eng. Khaled Ahmed |

## Quick Links

| Resource | Link |
| --- | --- |
| Mobile app repository | <https://github.com/Ala-Mahlak/Ala-Mahlak-Flutter> |
| Web dashboard repository | <https://github.com/Ala-Mahlak/Ala-Mahlak-Frontend> |
| Backend API repository | <https://github.com/Ala-Mahlak/Ala-Mahlak-Backend> |
| AI service repository | <https://github.com/Ala-Mahlak/Ala-Mahlak-AI> |
| Live backend Swagger | <https://ala-mahlak.runasp.net/swagger/index.html> |

---

<div align="center">

**Ala Mahlak - because every driver deserves to arrive safely.**

</div>
