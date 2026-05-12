# 🏋️ FormCheck AI

Real-time AI gym coach that uses computer vision to detect exercise form, count reps, and provide live voice coaching — all through your webcam.

## Demo

> [**Try it live →**](#) *(add your Streamlit deployment link)*

## What It Does

FormCheck AI watches you exercise through your webcam and:

- **Detects your pose** — Tracks 33 body landmarks in real-time using MediaPipe
- **Analyzes your form** — Calculates joint angles, checks depth, alignment, and flags errors
- **Coaches you with voice** — Generates natural coaching cues using an LLM and speaks them aloud
- **Counts reps and sets** — Automatic tracking with workout history saved per user

## Supported Exercises

| Exercise | What It Tracks |
|----------|---------------|
| Squats | Knee angle, back angle, depth status |
| Push-ups | Elbow angle, body alignment, hip position |
| Biceps Curls | Elbow angle, shoulder stability, swing detection |
| Shoulder Press | Elbow angle, arm extension, back arch |
| Lunges | Front knee angle, torso angle, balance status |

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Pose Detection | MediaPipe Pose Landmarker |
| Video Processing | OpenCV |
| Web Interface | Streamlit |
| Real-time Streaming | streamlit-webrtc + WebRTC |
| AI Coaching | Groq API + LLaMA 3.3 70B |
| Voice Synthesis | gTTS (Google Text-to-Speech) |
| Database | SQLite |
| Language | Python 3.11 |

## How It Works

1. **Webcam feed** is captured via WebRTC and processed frame-by-frame
2. **MediaPipe** extracts 33 pose landmarks from each frame
3. **Exercise detectors** calculate joint angles and detect rep stages (up/down)
4. **Form analysis** identifies errors (e.g., knees caving, hips sagging, back arching)
5. **Groq LLM** generates a short coaching cue based on the detected issue
6. **gTTS** converts the text to speech and plays it back in real-time
7. **SQLite** persists workout history per user

## Project Structure

```
├── main.py                          # App entry point
├── requirements.txt                 # Dependencies
├── .streamlit/config.toml           # Theme configuration
├── core/
│   └── base_exercise.py             # Abstract base class for exercises
├── detectors/
│   ├── squat.py                     # Squat detection logic
│   ├── pushup.py                    # Push-up detection logic
│   ├── biceps_curl.py               # Biceps curl detection logic
│   ├── shoulder_press.py            # Shoulder press detection logic
│   └── lunges.py                    # Lunge detection logic
├── ml_models/
│   └── pose_landmarker_full.task    # MediaPipe pose model
├── services/
│   ├── auth/login_wall.py           # User login
│   ├── coaching/
│   │   ├── llm.py                   # Groq LLM integration
│   │   ├── tts.py                   # Text-to-speech
│   │   └── voice_pipeline.py        # Voice coaching pipeline
│   ├── config/workout_config.py     # Exercise options & prompts
│   ├── persistence/exercise_repository.py  # SQLite database
│   ├── state/session_defaults.py    # Session state management
│   ├── tracking/metrics.py          # Rep/set tracking logic
│   ├── ui/style_loader.py           # CSS and font injection
│   └── vision/exercise_video_processor.py  # Video processing
└── static/
    ├── style.css                    # Custom styles
    └── AdobeClean.otf               # Custom font
```

## Setup

```bash
# Create conda environment
conda create -n gymcoach python=3.11 -y
conda activate gymcoach

# Install dependencies
pip install -r requirements.txt

# Add your Groq API key
# Create a .env file with: GROQ_API_KEY=your_key_here

# Run the app
streamlit run main.py
```

## Environment Variables

| Variable | Description |
|----------|------------|
| `GROQ_API_KEY` | API key from [console.groq.com](https://console.groq.com) |

## Built By

**Tejas Manoj** — Data & ML Engineer

- [LinkedIn](https://www.linkedin.com/in/iamteju/)
- [GitHub](https://github.com/iam-teju)
