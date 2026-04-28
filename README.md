# Face Recognition Based Attendance System

A Python-based attendance management system that uses real-time face recognition to automatically mark student attendance.

---

## Technologies Used

- **Python 3.10**
- **OpenCV** — Camera access and face detection (Haar Cascade)
- **OpenCV-contrib** — LBPH Face Recognizer
- **Tkinter** — GUI
- **Pandas** — CSV data management
- **Pillow** — Image processing
- **NumPy** — Numerical operations
- **Docker** — Containerization

---

## Project Structure

```
Project/
│
├── main.py                          # Main application
├── haarcascade_frontalface_default.xml  # Face detection model
├── Dockerfile                       # Docker configuration
├── requirements.txt                 # Python dependencies
├── README.md                        # Project documentation
│
├── TrainingImage/                   # Captured face images (auto-created)
├── TrainingImageLabel/              # Trained model - Trainner.yml (auto-created)
├── StudentDetails/                  # Student records CSV (auto-created)
└── Attendance/                      # Daily attendance CSVs (auto-created)
```

---

## How It Works

### Stage 1 — Register Face
- Enter Student ID and Name
- Click **Take Images**
- Camera opens and captures 100 face photos
- Photos saved to `TrainingImage/`
- Student details saved to `StudentDetails/StudentDetails.csv`

### Stage 2 — Train Model
- Click **Save Profile**
- LBPH algorithm reads all face photos
- Builds a mathematical face model
- Saves model to `TrainingImageLabel/Trainner.yml`

### Stage 3 — Take Attendance
- Click **Take Attendance**
- Camera opens and detects faces in real time
- Recognised faces are matched against trained model
- If confidence score < 50, attendance is marked
- Results saved to `Attendance/Attendance_DD-MM-YYYY.csv`
- Press **Q** to close camera and update attendance table

---

## Face Recognition Algorithm

**Haar Cascade** — Pre-trained face detector that scans every video frame for face-shaped light/shadow patterns.

**LBPH (Local Binary Pattern Histograms)** — For each pixel in a face image, compares it to its 8 neighbours and creates a binary texture fingerprint. Recognition works by comparing live face fingerprints against stored ones.

**Confidence Score** — Lower is better. Score of 0 = perfect match. Score above 50 = unknown face.

---

## Installation & Running Locally

### Prerequisites
- Python 3.10+
- Webcam

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/your-username/face-attendance-system.git
cd face-attendance-system

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the application
python main.py
```

---

## Docker Setup

> **Note:** This application uses a physical webcam and Tkinter GUI.
> Docker is used for containerization and dependency management.
> To run with camera access on Linux/Mac, use the commands below.

### Build the Docker Image

```bash
docker build -t face-attendance-system .
```

### Run the Container (Linux/Mac with display)

```bash
docker run -it \
  --device=/dev/video0 \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  face-attendance-system
```

### Run on Windows

On Windows, the application is best run directly with Python due to webcam and GUI limitations inside Docker containers. Docker is used here for dependency packaging and deployment documentation.

```bash
# Build image to verify all dependencies install correctly
docker build -t face-attendance-system .

# Run container in interactive mode
docker run -it face-attendance-system
```

---

## Features

- Real-time face detection using Haar Cascade
- Face recognition using LBPH algorithm
- Automatic duplicate prevention (same person marked only once per session)
- Auto-cleanup of duplicate student records on startup
- Attendance saved as daily CSV files
- Live attendance table in GUI
- Password-protected model training
- Camera runs in background thread (GUI stays responsive)

---

## Known Limitations

- Requires good lighting for accurate recognition
- Performance depends on webcam quality
- Docker container requires additional configuration for webcam access on Windows

---

## Developer

**Anas Shaikh**
