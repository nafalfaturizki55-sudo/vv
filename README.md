🚀 AI Trading Signal System (GitHub Actions + GitHub Pages)

📌 Overview

Proyek ini adalah sistem sinyal trading berbasis probabilitas yang:

- Mengambil data market (API)
- Menghitung indikator (EMA, RSI, MACD, Volume)
- Menghasilkan sinyal:
  - NAIK / TURUN
  - Probabilitas (%)
- Menampilkan hasil di dashboard web

✅ 100% gratis
✅ Tanpa server (pakai GitHub Actions)
✅ Aman (API key di GitHub Secrets)

---

🧠 Arsitektur Sistem

GitHub Actions (Backend)
        ↓
Fetch Data API
        ↓
Indicator Engine
        ↓
Scoring System
        ↓
Generate signal.json
        ↓
GitHub Pages (Frontend)
        ↓
Dashboard UI

---

📁 Struktur Project

/project-root
 ├── /data
 │    └── signal.json        # Output sinyal
 ├── /scripts
 │    └── main.py           # Logic utama (indikator + scoring)
 ├── index.html             # Dashboard
 ├── script.js              # Fetch & render data
 ├── style.css              # Styling
 └── .github/workflows/
      └── bot.yml           # GitHub Actions

---

⚙️ Setup Step-by-Step

1️⃣ Clone Repository

git clone https://github.com/username/project.git
cd project

---

2️⃣ Setup GitHub Secrets

Masuk ke:

Repo → Settings → Secrets → Actions

Tambahkan:

API_KEY=your_api_key

---

3️⃣ Script Python (Core Engine)

Contoh sederhana "scripts/main.py":

import requests
import json

def get_price():
    url = "https://api.binance.com/api/v3/ticker/price?symbol=BTCUSDT"
    return float(requests.get(url).json()['price'])

def calculate_signal(price):
    # contoh dummy logic
    if price % 2 == 0:
        return {"direction": "NAIK", "probability": 70}
    else:
        return {"direction": "TURUN", "probability": 60}

def main():
    price = get_price()
    signal = calculate_signal(price)

    data = {
        "symbol": "BTCUSDT",
        "price": price,
        "signal": signal
    }

    with open("data/signal.json", "w") as f:
        json.dump(data, f)

if __name__ == "__main__":
    main()

---

4️⃣ GitHub Actions Workflow

File: ".github/workflows/bot.yml"

name: Run Trading Bot

on:
  schedule:
    - cron: "*/10 * * * *"  # setiap 10 menit
  workflow_dispatch:

jobs:
  run-bot:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.10

      - name: Install dependencies
        run: pip install requests

      - name: Run script
        env:
          API_KEY: ${{ secrets.API_KEY }}
        run: python scripts/main.py

      - name: Commit result
        run: |
          git config --global user.name "bot"
          git config --global user.email "bot@github.com"
          git add data/signal.json
          git commit -m "update signal"
          git push

---

5️⃣ Dashboard (Frontend)

"index.html"

<!DOCTYPE html>
<html>
<head>
  <title>Trading Signal</title>
</head>
<body>
  <h1>BTC Signal</h1>
  <div id="output"></div>

  <script src="script.js"></script>
</body>
</html>

---

"script.js"

fetch("data/signal.json")
  .then(res => res.json())
  .then(data => {
    document.getElementById("output").innerHTML = `
      <p>Price: ${data.price}</p>
      <p>Direction: ${data.signal.direction}</p>
      <p>Probability: ${data.signal.probability}%</p>
    `;
  });

---

🌐 Deploy GitHub Pages

1. Masuk ke:

Settings → Pages

2. Pilih:

Branch: main
Folder: /root

3. Akses:

https://username.github.io/project

---

📊 Format Output JSON

{
  "symbol": "BTCUSDT",
  "price": 70200,
  "signal": {
    "direction": "NAIK",
    "probability": 75
  }
}

---

🔐 Security Notes

- ❌ Jangan taruh API key di frontend
- ✅ Gunakan GitHub Secrets
- ✅ Gunakan hanya di GitHub Actions

---

🚀 Roadmap Upgrade

V1 (sekarang)

- Single pair (BTC)
- Basic indikator
- JSON output

V2

- Multi-timeframe
- Multi-pair (ETH, SOL)
- Advanced scoring

V3

- Telegram notification
- Backtesting
- AI decision layer

---

🎯 Goal

Membangun:
👉 AI Trading Signal Platform

- Gratis
- Scalable
- Bisa dikembangkan ke produk

---

🤝 Contribution

Pull request terbuka untuk:

- Improve indikator
- UI dashboard
- Performance optimization

---

⚠️ Disclaimer

Sistem ini hanya untuk edukasi & eksperimen.
Gunakan dengan risiko masing-masing.

---

🔥 Next Step:

- Tambahkan EMA, RSI, MACD ke script
- Implement scoring system
- Uji akurasi sinyal
