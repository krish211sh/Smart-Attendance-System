# COER Smart Attendance

**Author:** Krishna Sharma, B.Tech CSE (Cyber Security), 1st Year, COER University, Roorkee

**Lecture-based, camera-driven attendance with proxy and spoof detection, prototype for COER University, Roorkee.**

> Status: interactive front-end prototype. All students, cameras and detections are **simulated** (fictional data). No real face recognition runs in this repository yet.

## Problem
Fake or proxy attendance is common in colleges. Manual roll calls and one-time entry marking cannot confirm that a student actually attended a particular lecture.

## Idea
Every classroom has a camera. For each timetable slot, only the camera of that lecture's room, during that period, can mark attendance.

- Recognized in the room on time: **Present**
- Recognized after the grace time: **Late**
- Seen only at the gate or elsewhere on campus: **Absent** (flagged as "on campus, not in class")
- Never recognized: **Absent** (faculty can review and override)

## Demo
Open `index.html` in any browser (no build, no dependencies).

1. Pick a lecture from the dropdown (CB308 C++, CB105 DBMS, Auditorium Guest Lecture).
2. Press **Start live simulation** to watch students being recognized in that room's camera.
3. Try **Simulate photo spoof** and **Simulate proxy** to see alerts.
4. Use the register search, filter and faculty **Toggle** override.

### Host free on GitHub Pages
1. Create a repository and upload all files from this folder.
2. Go to Settings, then Pages, choose branch `main` and folder `/ (root)`, and save.
3. Your site appears at `https://<username>.github.io/<repo>/`.

## Features
- Per-lecture attendance (room + time period)
- Room-camera binding (CB308, CB105, Auditorium)
- Bunk detection (on campus but not in class)
- Multi-camera face recognition with confidence score
- Liveness / anti-spoofing (photo, phone screen, video)
- Impossible-travel proxy alerts (same face in two rooms at once)
- Late marking with grace time, optional minimum presence (for example 75% of the lecture)
- Timetable sync, faculty dashboard with manual override
- Unknown-person alerts, reports and analytics, notifications to students and parents
- Student app: view attendance, correction requests, consent-based face enrollment
- Privacy by design: consent, encrypted embeddings, role-based access, audit logs, retention limits

## Planned architecture (real system)
```
Room cameras (RTSP) -> Frame sampler -> Face detection (RetinaFace / MediaPipe)
  -> Liveness check (anti-spoof CNN, blink / head-pose)
  -> Embedding (ArcFace / FaceNet) -> Match against enrolled students
  -> Rule engine (room + timetable + grace + presence %)
  -> Anomaly detection (Isolation Forest / rules) -> Alerts
  -> Database (PostgreSQL) -> Faculty dashboard / Student app / Reports
```

## Suggested tech stack
- Vision: Python, OpenCV, InsightFace or DeepFace, MediaPipe
- ML: scikit-learn (Isolation Forest, Random Forest / XGBoost), PyTorch
- Backend: FastAPI, PostgreSQL, Redis
- Frontend: this HTML prototype, later React or Flutter
- Datasets for liveness research: CASIA-FASD, Replay-Attack

## Roadmap
1. Backend with face enrollment and recognition on webcam
2. Liveness detection module
3. Timetable and room-camera mapping
4. Proxy / anomaly detection on attendance logs
5. Faculty dashboard connected to real data
6. Mobile app and notifications

## Privacy and ethics
Face data is sensitive. Use only with written consent, store embeddings (not photos) encrypted, restrict access, keep audit logs, define a retention period, and always provide a human review path. No system is 100% accurate.

## License
MIT, see `LICENSE`.

