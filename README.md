# 🔊 VoxForge — Text-to-Speech Portal

Convert any text into a downloadable **MP3** audio file with **male and female
voices**. Built with **Next.js (App Router)**, **PostgreSQL + Drizzle ORM**, and
a **Python speech engine**.

## ✨ Features

- 👩 Female / 👨 Male / 🧑 Neutral voices (real pitch-shifted speech)
- 7 English accents (US, UK, AU, IN, CA, IE, ZA)
- Normal / slow speed toggle
- In-browser audio player + one-click MP3 download
- Persistent conversion history (PostgreSQL)

## 🧠 How the speech engine works

`scripts/tts.py` runs a real audio pipeline:

1. **gTTS** synthesizes intelligible speech (MP3)
2. **miniaudio** decodes it to PCM
3. **numpy** pitch-shifts the waveform to create distinct male / female voices
4. **lameenc** re-encodes to a downloadable MP3

The Next.js API route (`src/lib/tts.ts`) spawns the Python script and streams the
result back to the browser.

## 🚀 Getting started

### Prerequisites

- Node.js 18+
- Python 3.10+
- PostgreSQL

### Install

```bash
# JS dependencies
npm install

# Python dependencies
pip install -r requirements.txt
```

### Configure environment

Create a `.env` file:

```env
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1:5432/app_db
```

### Set up the database

```bash
npx drizzle-kit push
```

### Run

```bash
npm run dev
```

Open http://localhost:3000

## 🗂️ Project structure

```
scripts/tts.py                     # Python speech engine
requirements.txt                   # Python dependencies
src/lib/tts.ts                     # Node ↔ Python bridge
src/app/api/synthesize/route.ts    # Text → MP3 endpoint
src/app/api/history/                # Conversion history endpoints
src/components/TtsPortal.tsx        # UI
src/db/schema.ts                   # Drizzle schema
```

## 📝 License

MIT
