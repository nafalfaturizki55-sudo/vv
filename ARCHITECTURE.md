🏗️ ARCHITECTURE.md

AI Trading Signal System (Serverless - GitHub Actions + GitHub Pages)

---

🧠 1. OVERVIEW

Dokumen ini menjelaskan arsitektur teknis lengkap dari sistem:

👉 AI Trading Signal Engine (Signal Only)

Karakteristik:

- Serverless (tanpa VPS)
- Modular
- Scalable
- Berbasis batch processing (cron)

---

🎯 2. HIGH LEVEL ARCHITECTURE

          ┌───────────────┐
          │ External APIs │
          │ (Market Data) │
          └──────┬────────┘
                 ↓
        ┌──────────────────┐
        │ Data Fetch Layer │
        └──────┬───────────┘
               ↓
      ┌────────────────────┐
      │ Indicator Engine   │
      └──────┬─────────────┘
             ↓
      ┌────────────────────┐
      │ Scoring Engine     │
      └──────┬─────────────┘
             ↓
      ┌────────────────────┐
      │ Probability Engine │
      └──────┬─────────────┘
             ↓
      ┌────────────────────┐
      │ Signal Generator   │
      └──────┬─────────────┘
             ↓
      ┌────────────────────┐
      │ JSON Storage       │
      └──────┬─────────────┘
             ↓
      ┌────────────────────┐
      │ Frontend (Web UI)  │
      └────────────────────┘

---

🧩 3. SYSTEM COMPONENTS

---

🔌 3.1 Data Fetch Layer

📌 Fungsi

Mengambil data market dari API eksternal

📥 Input

- Symbol (BTCUSDT)
- Timeframe (10m, 30m, 1H, 1D)

📤 Output

[
  {
    "time": "...",
    "open": 70000,
    "high": 70500,
    "low": 69800,
    "close": 70200,
    "volume": 1200
  }
]

📁 File

/scripts/data_fetch.py

---

📊 3.2 Indicator Engine

📌 Fungsi

Menghitung indikator teknikal dari data OHLC

📥 Input

- Data OHLC
- Volume

📤 Output

{
  "ema20": 70100,
  "ema50": 69500,
  "rsi": 48.5,
  "macd": {
    "value": 10,
    "signal": 8
  },
  "volume_trend": "UP"
}

📁 Struktur

/scripts/indicators/
 ├── ema.py
 ├── rsi.py
 ├── macd.py
 └── volume.py

---

🧮 3.3 Scoring Engine

📌 Fungsi

Mengubah indikator menjadi skor numerik

📥 Input

- Output indikator

📤 Output

{
  "trend": 40,
  "momentum": 20,
  "macd": 15,
  "volume": 5,
  "total": 80
}

📁 File

/scripts/scoring.py

---

📈 3.4 Probability Engine

📌 Fungsi

Mengubah skor menjadi probabilitas & arah

📥 Input

- Total score

📤 Output

{
  "direction": "NAIK",
  "probability": 80,
  "strength": "STRONG"
}

📁 File

/scripts/probability.py

---

🚦 3.5 Signal Generator

📌 Fungsi

Menggabungkan semua hasil menjadi sinyal final

📥 Input

- Data indikator
- Skor
- Probabilitas

📤 Output

{
  "symbol": "BTCUSDT",
  "timeframe": "1H",
  "signal": {
    "direction": "NAIK",
    "probability": 80,
    "strength": "STRONG"
  },
  "timestamp": "2026-03-31T13:00:00Z"
}

📁 File

/scripts/signal.py

---

🧠 3.6 Core Engine (Orchestrator)

📌 Fungsi

Mengatur alur seluruh sistem

Flow:

fetch_data → indicators → scoring → probability → signal → save

📁 File

/scripts/main.py

---

💾 3.7 Storage Layer

📌 Fungsi

Menyimpan hasil sinyal

Format

- JSON

Lokasi

/data/signal.json

---

🤖 3.8 Automation Layer (GitHub Actions)

📌 Fungsi

Menjalankan sistem otomatis

Trigger

- Cron schedule
- Manual trigger

Flow:

checkout → setup → run script → commit → push

📁 File

.github/workflows/bot.yml

---

🌐 3.9 Frontend Layer (GitHub Pages)

📌 Fungsi

Menampilkan sinyal ke user

Teknologi

- HTML
- CSS
- JavaScript

Data Source

/data/signal.json

📁 Struktur

/web/
 ├── index.html
 ├── script.js
 └── style.css

---

🔄 4. DATA FLOW DETAIL

1. GitHub Actions trigger
2. main.py dijalankan
3. data_fetch ambil OHLC
4. indikator dihitung
5. scoring dihitung
6. probabilitas ditentukan
7. signal.json di-generate
8. commit ke repo
9. GitHub Pages update UI

---

🧱 5. MODULAR DESIGN PRINCIPLES

- Single Responsibility per module
- Loose coupling antar module
- Easy to replace components
- Scalable for future upgrade

---

🔐 6. SECURITY ARCHITECTURE

API Key

- Disimpan di GitHub Secrets
- Tidak ada di frontend

Access Flow

GitHub Actions → API → Process → Output

---

⚡ 7. PERFORMANCE DESIGN

Target:

- Execution < 60 detik
- Memory ringan
- Stateless (tidak simpan state di server)

---

📦 8. DEPLOYMENT ARCHITECTURE

GitHub Repo
   ├── Actions (compute)
   ├── Data (JSON)
   └── Pages (UI)

---

🔧 9. EXTENSIBILITY

Sistem bisa dikembangkan ke:

V2

- Multi pair (ETH, SOL)
- Multi API

V3

- Machine Learning
- Adaptive scoring

V4

- Real-time streaming
- Dedicated backend server

---

⚠️ 10. LIMITATIONS

- Tidak real-time (cron-based)
- Bergantung API eksternal
- Tidak cocok untuk HFT
- Tidak ada state persistence

---

🧠 11. DESIGN PHILOSOPHY

- Simplicity over complexity
- Signal clarity over noise
- Scalability from start
- Zero-cost infrastructure

---

🎯 12. FINAL SUMMARY

Arsitektur ini dirancang untuk:

✔ Gratis
✔ Modular
✔ Mudah dikembangkan
✔ Siap di-scale

👉 Menjadi fondasi:
AI Trading Signal Platform

---
