📄 SPESIFIKASI SISTEM

AI Trading Signal Engine (GitHub Actions + GitHub Pages)

---

🧠 1. TUJUAN SISTEM

Membangun sistem yang mampu:

- Menghasilkan sinyal prediksi market
- Output berupa:
  - Arah: NAIK / TURUN / NO TRADE
  - Probabilitas (%)
- Mendukung multi-timeframe:
  - 10 menit
  - 30 menit
  - 1 jam
  - 1 hari
- Berjalan otomatis tanpa server (serverless)

---

🎯 2. RUANG LINGKUP

Termasuk:

- Pengambilan data market (API)
- Perhitungan indikator teknikal
- Sistem scoring & probabilitas
- Penyimpanan hasil (JSON)
- Dashboard web statis

Tidak termasuk:

- Eksekusi trading (order buy/sell)
- Manajemen portofolio
- High-frequency trading

---

🏗️ 3. ARSITEKTUR SISTEM

[ External API ]
      ↓
[ Data Fetch Layer ]
      ↓
[ Indicator Engine ]
      ↓
[ Scoring Engine ]
      ↓
[ Probability Engine ]
      ↓
[ Signal Generator ]
      ↓
[ JSON Storage ]
      ↓
[ Frontend Dashboard ]

---

🔌 4. DATA SOURCE

4.1 Data Utama

- OHLC (Open, High, Low, Close)
- Volume
- Timestamp

4.2 Endpoint (contoh)

- Binance REST API:
  - "/api/v3/klines"
- Alternatif:
  - MEXC API
  - CoinGecko API

4.3 Interval Data

Timeframe| Interval API
10m| 10m
30m| 30m
1H| 1h
1D| 1d

---

⚙️ 5. INDICATOR ENGINE

5.1 Indikator Wajib

EMA (Exponential Moving Average)

- EMA 20
- EMA 50

RSI (Relative Strength Index)

- Period: 14

MACD

- Fast: 12
- Slow: 26
- Signal: 9

Volume

- Raw volume
- Moving average volume (optional)

---

5.2 Output Indicator

{
  "ema20": 70200,
  "ema50": 69800,
  "rsi": 45.2,
  "macd": {
    "value": 12.5,
    "signal": 10.2
  },
  "volume": 1200
}

---

🧮 6. SCORING ENGINE

6.1 Range Skor

- Minimum: -100
- Maximum: +100

---

6.2 Aturan Scoring

Trend

- Harga > EMA50 → +25
- Harga < EMA50 → -25
- EMA20 > EMA50 → +15
- EMA20 < EMA50 → -15

---

Momentum (RSI)

- RSI < 35 → +20
- RSI > 65 → -20
- RSI 35–65 → 0

---

MACD

- MACD > Signal → +20
- MACD < Signal → -20

---

Volume

- Volume naik signifikan → +10
- Volume turun → -10

---

6.3 Total Skor

score = trend + momentum + macd + volume

---

📊 7. PROBABILITY ENGINE

7.1 Konversi Skor

probability = abs(score)

---

7.2 Direction

if score > 0 → NAIK
if score < 0 → TURUN
if -40 < score < 40 → NO TRADE

---

7.3 Threshold

Skor| Output
70–100| Strong Signal
40–69| Weak Signal
-39–39| No Trade

---

🚦 8. SIGNAL GENERATOR

8.1 Format Output

{
  "symbol": "BTCUSDT",
  "timeframe": "1H",
  "signal": {
    "direction": "NAIK",
    "probability": 75,
    "strength": "STRONG"
  },
  "timestamp": "2026-03-31T13:00:00Z"
}

---

8.2 Multi-Timeframe Output

{
  "BTCUSDT": {
    "10m": { "direction": "NAIK", "probability": 65 },
    "30m": { "direction": "NAIK", "probability": 70 },
    "1H": { "direction": "NAIK", "probability": 80 },
    "1D": { "direction": "TURUN", "probability": 55 }
  }
}

---

💾 9. STORAGE

9.1 Format

- JSON file
- Lokasi:

/data/signal.json

---

9.2 Update Mechanism

- Overwrite setiap eksekusi
- Commit ke repository

---

🤖 10. AUTOMATION (GitHub Actions)

10.1 Trigger

- Schedule (cron)
- Manual trigger

10.2 Interval

Timeframe| Cron
10m| */10 * * * *
30m| */30 * * * *
1H| 0 * * * *
1D| 0 0 * * *

---

10.3 Workflow Step

1. Checkout repo
2. Setup environment
3. Install dependencies
4. Run script
5. Save JSON
6. Commit & push

---

🌐 11. FRONTEND (GitHub Pages)

11.1 Fitur

- Tampilkan sinyal
- Multi-timeframe view
- Last update time

---

11.2 Data Source

/data/signal.json

---

11.3 Output UI

- Symbol (BTCUSDT)
- Direction
- Probability
- Status (Bullish/Bearish)

---

🔐 12. SECURITY

12.1 API Key

- Disimpan di GitHub Secrets
- Tidak boleh di frontend

12.2 Akses

- Backend only (GitHub Actions)

---

📈 13. PERFORMANCE

Target:

- Execution time < 60 detik
- Data latency < 5 menit
- Availability: tergantung GitHub uptime

---

⚠️ 14. LIMITASI

- Tidak real-time (delay tergantung cron)
- Tidak cocok untuk scalping cepat
- Bergantung pada API eksternal
- Tidak ada machine learning (versi dasar)

---

🚀 15. ROADMAP

V1 (Current)

- Single pair
- Basic indikator
- Manual scoring

V2

- Multi pair
- Advanced indikator
- Better scoring

V3

- Machine learning
- Adaptive probability
- Signal optimization

---

🧪 16. TESTING

16.1 Backtesting

- Gunakan data historis
- Simulasi sinyal

16.2 Validation

- Hitung winrate
- Evaluasi akurasi

---

📌 17. DEFINISI ISTILAH

- NAIK → Prediksi harga naik
- TURUN → Prediksi harga turun
- NO TRADE → Tidak ada sinyal
- Probabilitas → Kekuatan sinyal (%)

---

🎯 18. KRITERIA SUKSES

- Sistem menghasilkan sinyal konsisten
- Probabilitas representatif terhadap hasil
- Bisa berjalan otomatis tanpa error

---

🔥 PENUTUP

Spesifikasi ini menjadi dasar untuk:
👉 pengembangan sistem sinyal trading berbasis probabilitas
👉 scalable menjadi AI trading platform

---
