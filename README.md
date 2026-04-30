# 🎓 SmartAttend — AI-Powered Face Recognition Attendance System

A production-ready Smart Attendance System built with **Python**, **Flask**, **OpenCV**, and **face_recognition** (ageitgey). Features real-time webcam-based attendance marking, anti-spoofing via blink detection, role-based dashboards, analytics, Excel export, and email alerts.

---
<img width="1236" height="702" alt="Screenshot 2026-04-30 at 11 26 05 PM" src="https://github.com/user-attachments/assets/bfe72bdd-b21d-47e2-8a05-1537d28eb9f0" />
<img width="1271" height="745" alt="Screenshot 2026-04-30 at 11 25 01 PM" src="https://github.com/user-attachments/assets/2fed5da3-c66a-49c0-a1d4-b0ffb22213c7" />
<img width="1246" height="695" alt="Screenshot 2026-04-30 at 11 28 02 PM" src="https://github.com/user-attachments/assets/4fe07726-4484-486e-a5fa-7bdb73ed976d" />
<img width="1268" height="742" alt="Screenshot 2026-04-30 at 11 28 43 PM" src="https://github.com/user-attachments/assets/c26ef6f8-86fb-4d37-9269-b81d16de4354" />
<img width="1264" height="653" alt="Screenshot 2026-04-30 at 11 30 46 PM" src="https://github.com/user-attachments/assets/9f06da0a-69fc-4c80-a2f8-e983b9d70d22" />


## 🚀 Features

| Feature | Description |
|---------|-------------|
| 🤖 Face Recognition | Real-time face detection & 128-d encoding matching |
| 🛡️ Anti-Spoofing | Eye blink detection (EAR method) to reject photos |
| 👥 Role-Based Auth | Admin, Teacher, Student with separate dashboards |
| 📊 Analytics | Attendance %, low-attendance highlighting, subject-wise stats |
| 📸 Image Logging | Every face capture is saved with timestamp |
| 📧 Email Alerts | SMTP alerts for students below 75% attendance |
| 📥 Excel Export | Beautiful formatted attendance reports |
| 🚫 Fraud Prevention | Duplicate detection, unknown face handling, multi-face alerts |

---

## 📁 Project Structure

```
smart-attendance/
├── config.py              # Central configuration
├── run.py                 # Flask entry point
├── requirements.txt       # Dependencies
├── app/
│   ├── __init__.py        # App factory
│   ├── extensions.py      # DB, Login Manager
│   ├── models/            # SQLAlchemy models
│   ├── routes/            # Flask blueprints (auth, teacher, student, admin)
│   ├── services/          # Business logic (attendance, export, alerts)
│   ├── face_module/       # Face detection, recognition, anti-spoofing, camera
│   ├── templates/         # Jinja2 HTML templates
│   └── static/            # CSS, JS, captured images
├── database/
│   └── seed.py            # Demo data seeder
└── data/
    └── known_faces/       # Registered student face images
```

---

## 🛠️ Setup Instructions

### Prerequisites

- **Python 3.10+**
- **CMake** (required for dlib): `pip install cmake`
- **Visual Studio Build Tools** (Windows) — for compiling dlib
- Webcam (for attendance sessions)

### Step 1: Clone & Setup

```bash
cd "Major Project"  # Your project directory
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux
```

### Step 2: Install Dependencies

```bash
pip install cmake
pip install dlib
pip install -r requirements.txt
```

> ⚠️ **Note:** `dlib` can be difficult to install on Windows. If you encounter issues:
> 1. Install Visual Studio Build Tools (C++ workload)
> 2. Or use `conda install -c conda-forge dlib`

### Step 3: Download Anti-Spoofing Model (Optional)

For blink detection, download the dlib landmark predictor:

```bash
# Download shape_predictor_68_face_landmarks.dat
# From: http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2
# Extract and place in: data/shape_predictor_68_face_landmarks.dat
```

> The system works without it — blink detection will simply be skipped.

### Step 4: Seed the Database

```bash
python database/seed.py
```

### Step 5: Run the Application

```bash
python run.py
```

Open **http://localhost:5000** in your browser.

---

## 🔑 Demo Credentials

| Role    | Email                    | Password     |
|---------|--------------------------|-------------|
| Admin   | admin@university.edu     | admin123    |
| Teacher | sharma@university.edu    | teacher123  |
| Student | rohan@student.edu        | student123  |

---

## 📋 Usage Guide

### Admin
1. Login as Admin
2. Add Teachers, Students (with face photo), and Subjects
3. Face photos are auto-encoded during registration

### Teacher
1. Login → Select semester
2. Click **Start Session** on a subject
3. Webcam activates — students appear in front of camera
4. System auto-detects, recognizes, and marks attendance
5. Click **End Session** when done
6. Export attendance to Excel or send low-attendance alerts

### Student
1. Login → View attendance dashboard
2. See overall %, subject-wise stats, and attendance history
3. Receive email alerts if attendance drops below 75%

---

## ⚙️ Configuration

Edit `config.py` to tune:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `FACE_RECOGNITION_TOLERANCE` | `0.45` | Lower = stricter face matching |
| `FRAME_RESIZE_FACTOR` | `0.25` | Smaller = faster processing |
| `PROCESS_EVERY_N_FRAMES` | `2` | Skip frames for speed |
| `EAR_THRESHOLD` | `0.21` | Blink sensitivity |
| `BLINK_REQUIRED_COUNT` | `2` | Blinks to verify liveness |
| `LOW_ATTENDANCE_THRESHOLD` | `75` | Alert trigger (%) |
| `DUPLICATE_WINDOW_MINUTES` | `60` | Prevent re-marking window |

---

## 🧪 Tech Stack

- **Backend:** Flask, SQLAlchemy, Flask-Login
- **Face Recognition:** face_recognition (ageitgey), OpenCV, dlib
- **Anti-Spoofing:** Eye Aspect Ratio (EAR) blink detection
- **Database:** SQLite (scalable to PostgreSQL)
- **Frontend:** HTML5, CSS3 (custom dark theme), JavaScript
- **Export:** openpyxl
- **Alerts:** Python smtplib

---

## 📜 License

This project is for educational purposes (university major project).
