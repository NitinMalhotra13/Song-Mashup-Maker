# Song Mashup Maker

Song Mashup Maker is a Python project that automatically creates a music mashup from YouTube videos of a given singer.  
It provides **two ways** to use the system:

- **Part 1 – Command Line Interface (CLI)**
- **Part 2 – Web Service (Streamlit UI)**

The application downloads videos, converts them to audio, trims them, merges them into a single mashup, and (in the web version) zips and emails the result.

---

## Repository Structure

```
Song-Mashup-Maker/
│
├── part1-cli/
│   └── 102303918.py        # CLI Mashup Generator
│
├── part2-webservice/
│   └── app.py              # Streamlit Web App
│
├── requirements.txt        # Python Dependencies
├── test.mp3                # Example Output File
└── README.md
```

---

## Core Functionality

- Download MP4 videos from YouTube
- Convert videos to MP3 audio
- Trim the first *N* seconds from each audio
- Merge all audio clips into one mashup
- ZIP the final mashup (Web version)
- Send mashup via email (Web version)
- Automatic cleanup of temporary files

---

## Part 1 – CLI Application

Run directly from terminal with arguments.

### Usage
```bash
python part1-cli/102303918.py "Singer Name" <NumberOfVideos> <DurationSeconds> <OutputFile>
```

### Example
```bash
python part1-cli/102303918.py "Arijit Singh" 12 30 mashup.mp3
```

---

## Part 2 – Web Service (Streamlit)

Interactive web interface for generating mashups.

### Run
```bash
pip install -r requirements.txt
streamlit run part2-webservice/app.py
```

Then open in browser:
```
http://localhost:8501
```

---

## Installation

Install Python dependencies:

```bash
pip install -r requirements.txt
```

### System Requirement
- **FFmpeg** must be installed and added to PATH.

Verify installation:
```bash
ffmpeg -version
```

---

## 📧 Email Setup (Web Version)

Before running the web app, update sender email credentials in `app.py`:

```python
sender_email = "yourgmail@gmail.com"
app_password = "YOUR_APP_PASSWORD"
```

Use a **Gmail App Password**, not your actual Gmail password.

---

## Cleanup / Clear Function

The project contains a `cleanup()` function that removes temporary folders and files created during processing:

```python
def cleanup():
    folders = ["downloads", "mp3", "trimmed"]
    files = ["mashup.zip", "mashup.mp3"]

    for f in folders:
        if os.path.exists(f):
            shutil.rmtree(f)

    for file in files:
        if os.path.exists(file):
            os.remove(file)
```

### Purpose
- Deletes intermediate video/audio folders
- Removes temporary mashup ZIP and MP3 files
- Keeps the project directory clean after each run

---

##  Libraries Used

| Purpose | Library |
|--------|--------|
| YouTube Download | `yt-dlp` |
| Video → Audio Conversion | `moviepy` |
| Audio Processing | `pydub` |
| Web Interface | `streamlit` |

Standard Python libraries are used for ZIP compression and email handling.

---

## Notes
- First run may take longer due to video downloads.
- Stable internet connection recommended.
- Designed as a demonstration of multimedia processing using Python.
