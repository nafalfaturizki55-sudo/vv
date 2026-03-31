📋 TASK.md

AI Trading Signal System — From Zero to Production

---

🧭 OVERVIEW

Dokumen ini adalah task list lengkap (end-to-end) untuk membangun sistem:

👉 AI Trading Signal Engine (Signal Only)
Mulai dari setup → development → testing → production

---

🟢 PHASE 0 — PROJECT SETUP

🎯 Tujuan

Menyiapkan environment dan struktur awal

Tasks

- [ ] Create GitHub repository
- [ ] Setup folder structure:
  /data
/scripts
/web
/.github/workflows
- [ ] Create base files:
  - [ ] README.md
  - [ ] spesifikasi.md
  - [ ] TASK.md
- [ ] Setup ".gitignore" (Python + Node)
- [ ] Setup Python environment (3.10+)

---

🟢 PHASE 1 — DATA ENGINE

🎯 Tujuan

Mengambil data market dari API

Tasks

- [ ] Create file: "scripts/data_fetch.py"
- [ ] Implement function:
  - [ ] fetch_ohlc(symbol, timeframe)
- [ ] Support timeframe:
  - [ ] 10m
  - [ ] 30m
  - [ ] 1h
  - [ ] 1d
- [ ] Normalize response ke format:

{
  "time": "",
  "open": 0,
  "high": 0,
  "low": 0,
  "close": 0,
  "volume": 0
}

---

🟡 PHASE 2 — INDICATOR ENGINE

🎯 Tujuan

Menghitung indikator teknikal

Tasks

- [ ] Create folder: "/scripts/indicators"

EMA

- [ ] Create "ema.py"
- [ ] Implement:
  - [ ] ema(data, period)

RSI

- [ ] Create "rsi.py"
- [ ] Implement:
  - [ ] rsi(data, period=14)

MACD

- [ ] Create "macd.py"
- [ ] Implement:
  - [ ] macd(data)

Volume

- [ ] Implement:
  - [ ] volume trend detection

---

🟠 PHASE 3 — SCORING ENGINE

🎯 Tujuan

Mengubah indikator menjadi skor

Tasks

- [ ] Create file: "scripts/scoring.py"

Implement:

- [ ] trend_score()
- [ ] momentum_score()
- [ ] macd_score()
- [ ] volume_score()

Combine:

- [ ] total_score()

---

🔵 PHASE 4 — PROBABILITY ENGINE

🎯 Tujuan

Mengubah skor menjadi probabilitas & sinyal

Tasks

- [ ] Create file: "scripts/probability.py"

Implement:

- [ ] score_to_probability()
- [ ] determine_direction()
- [ ] determine_strength()

---

🔴 PHASE 5 — SIGNAL GENERATOR

🎯 Tujuan

Menghasilkan output final

Tasks

- [ ] Create file: "scripts/signal.py"

Implement:

- [ ] generate_signal(symbol, timeframe)
- [ ] multi_timeframe_signal()

Output:

- [ ] JSON format ("data/signal.json")

---

🟣 PHASE 6 — INTEGRATION (CORE ENGINE)

🎯 Tujuan

Menggabungkan semua module

Tasks

- [ ] Create "scripts/main.py"

- [ ] Pipeline:
  
  - fetch data
  - calculate indicators
  - scoring
  - probability
  - generate JSON

- [ ] Support:
  
  - [ ] BTCUSDT
  - [ ] Multi-timeframe

---

🟤 PHASE 7 — AUTOMATION (GitHub Actions)

🎯 Tujuan

Menjalankan sistem otomatis

Tasks

- [ ] Create ".github/workflows/bot.yml"

- [ ] Setup cron:
  
  - [ ] 10 menit
  - [ ] 30 menit
  - [ ] 1 jam

- [ ] Steps:
  
  - checkout
  - setup python
  - install dependencies
  - run script
  - commit JSON

---

⚫ PHASE 8 — FRONTEND DASHBOARD

🎯 Tujuan

Menampilkan sinyal

Tasks

- [ ] Create "/web/index.html"

- [ ] Create "/web/script.js"

- [ ] Fetch "signal.json"

- [ ] Display:
  
  - symbol
  - timeframe
  - direction
  - probability

- [ ] Add:
  
  - [ ] last update time
  - [ ] simple styling

---

⚪ PHASE 9 — TESTING

🎯 Tujuan

Validasi sistem

Tasks

- [ ] Unit test:
  
  - [ ] EMA
  - [ ] RSI
  - [ ] MACD

- [ ] Integration test:
  
  - [ ] full pipeline

- [ ] Manual validation:
  
  - [ ] bandingkan dengan chart

---

🧪 PHASE 10 — BACKTESTING (IMPORTANT)

🎯 Tujuan

Mengetahui akurasi

Tasks

- [ ] Create "backtest.py"
- [ ] Input data historis
- [ ] Simulasi sinyal
- [ ] Output:
  - winrate
  - profit/loss

---

🚀 PHASE 11 — OPTIMIZATION

🎯 Tujuan

Meningkatkan performa

Tasks

- [ ] Optimize scoring weight
- [ ] Reduce noise signal
- [ ] Improve threshold

---

🛡️ PHASE 12 — SECURITY

🎯 Tujuan

Menjaga keamanan sistem

Tasks

- [ ] Setup GitHub Secrets
- [ ] Remove hardcoded API key
- [ ] Validate API response

---

🌍 PHASE 13 — DEPLOYMENT

🎯 Tujuan

Menjalankan sistem publik

Tasks

- [ ] Enable GitHub Pages
- [ ] Set branch deployment
- [ ] Test public access

---

📊 PHASE 14 — MONITORING

🎯 Tujuan

Memastikan sistem berjalan stabil

Tasks

- [ ] Check GitHub Actions logs
- [ ] Track failures
- [ ] Add logging system

---

🔔 PHASE 15 — NOTIFICATION (OPTIONAL)

🎯 Tujuan

Mengirim sinyal otomatis

Tasks

- [ ] Integrate Telegram bot
- [ ] Send signal alert

---

🧠 PHASE 16 — ADVANCED (FUTURE)

🎯 Tujuan

Upgrade ke level AI

Tasks

- [ ] Multi-API integration
- [ ] Machine learning model
- [ ] Adaptive scoring

---

🎯 FINAL CHECKLIST (PRODUCTION READY)

- [ ] Sistem jalan otomatis (cron OK)
- [ ] JSON update normal
- [ ] Dashboard tampil
- [ ] Tidak ada error di logs
- [ ] Probabilitas konsisten
- [ ] Winrate terukur

---

🔥 END GOAL

👉 Sistem berjalan:

- otomatis
- stabil
- scalable

👉 Siap dikembangkan menjadi:
AI Trading Signal Platform

---
