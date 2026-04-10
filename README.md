<div align="center">

# 💱 Exchange Converter — AI Edge Skill

[![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)](https://github.com/esvialv/exchange-converter/releases)
[![Model](https://img.shields.io/badge/model-Gemma--4--E4B--it-orange?style=flat-square&logo=google)](https://ai.google.dev/edge)
[![Platform](https://img.shields.io/badge/platform-AI_Edge_Gallery-4285F4?style=flat-square&logo=android)](https://github.com/google-ai-edge)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)
[![Privacy](https://img.shields.io/badge/privacy-100%25_on--device-darkgreen?style=flat-square)](SKILL.md)
[![GitHub Stars](https://img.shields.io/github/stars/esvialv/exchange-converter?style=flat-square&logo=github)](https://github.com/esvialv/exchange-converter)

**A real-time currency & crypto converter skill for Google AI Edge Gallery.**  
Powered by **Gemma 4** running locally on your device. Fetches live rates when online, falls back to cached rates when offline.

[📋 SKILL.md](SKILL.md) · [🐛 Report an Issue](https://github.com/esvialv/exchange-converter/issues)

</div>

---

## 🏆 Why Exchange Converter?

| Feature | Calculator Apps | Web Converters | **Exchange Converter** |
|---|:---:|:---:|:---:|
| Natural language input | ❌ | ❌ | ✅ |
| Crypto + Fiat in one tool | ❌ | ⚠️ | ✅ |
| Works 100% offline (cached) | ❌ | ❌ | ✅ |
| No cloud / No tracking | ❌ | ❌ | ✅ |
| Runs on-device with Gemma 4 | ❌ | ❌ | ✅ |
| Flag emoji formatting | ❌ | ❌ | ✅ |

---

## ✨ Key Features

- **Fiat & Crypto Support** — Convert between 150+ fiat currencies (USD, EUR, GBP, JPY, MXN…) and hundreds of cryptocurrencies (BTC, ETH, SOL, DOGE, ADA…).
- **Natural Language Understanding** — Just say "How much is 100 USD in EUR?" or "Convert 0.5 BTC to GBP". Gemma 4 handles the parsing.
- **Offline-First Architecture** — Rates are cached locally after the first fetch. No internet? No problem — cached rates kick in automatically.
- **Live Exchange Rates** — Fetches real-time rates from multiple redundant APIs with automatic failover.
- **Zero Data Collection** — Everything runs on-device via Gemma 4. No data leaves your phone.

---

## 🔧 How It Works

Exchange Converter is a **Skill** for the [Google AI Edge Gallery](https://github.com/google-ai-edge) app, designed to run with the **Gemma 4 E4B-it** model locally on Android/iOS devices.

```
User prompt ──► Gemma 4 (on-device) ──► Parses intent & currencies
                                          │
                                          ▼
                                    run_js (index.html)
                                          │
                              ┌───────────┴───────────┐
                              ▼                       ▼
                        Live API fetch          Local cache
                        (when online)         (when offline)
                              │                       │
                              └───────────┬───────────┘
                                          ▼
                                  Formatted result
                                 returned to Gemma 4
                                          │
                                          ▼
                                  User sees output:
                          🇺🇸 100.00 USD → 🇪🇺 92.35 EUR
```

1. **You speak naturally** — "Convert 100 dollars to euros" or "How much is 1 BTC in JPY?"
2. **Gemma 4 parses your request** — The on-device LLM extracts the action, amount, source currency, and target currency from your message.
3. **JavaScript engine executes** — The skill calls `run_js` with structured JSON. The embedded script fetches live rates (or uses cached ones) and performs the conversion.
4. **Gemma 4 formats the response** — The model reads the JSON result and outputs a clean, emoji-rich response.

---

## 🚀 Installation

### Option 1: Import from URL (Recommended)
1. Open **Google AI Edge Gallery** on your Android/iOS device.
2. Tap **Agent Skills** → **Add Custom Skill** → **From URL**.
3. Paste this URL:
```
https://github.com/esvialv/exchange-converter
```
4. Confirm. The skill will load and activate **Exchange Converter v1.0.0**.

### Option 2: Clone locally
```bash
git clone https://github.com/esvialv/exchange-converter.git
```
Point AI Edge Gallery to the local folder (see app documentation).

---

## 💬 Usage Examples

> Just talk to the agent naturally. Here are some examples:

**🔄 Convert Currencies**
- `"100 USD to EUR"`
- `"How much is 50 euros in Japanese yen?"`
- `"500 MXN to dollars"`

**₿ Convert Crypto**
- `"Convert 0.5 BTC to USD"`
- `"How much is 1 ETH in EUR?"`
- `"1000 DOGE to GBP"`

**📋 List & Help**
- `"What currencies are available?"`
- `"Help"` / `"What can you do?"`

---

## 💬 Live Agent Response Example

Below is a real example of what Exchange Converter produces:

> *"Convert 100 USD to EUR"*

```
🇺🇸 100.00 USD → 🇪🇺 92.35 EUR
📊 1 USD = 0.923500 EUR
📅 2026-04-10
```

> *"0.5 BTC to GBP"* (offline)

```
🇧🇹 0.50 BTC → 🇬🇧 32450.00 GBP
📊 1 BTC = 64900.000000 GBP
📅 2026-04-09
⚠️ Offline — cached rates from 2026-04-09
```

---

## 🗂 Repository Structure

```text
exchange-converter/
├── SKILL.md              # Skill definition & system prompt
├── README.md             # This file
└── scripts/
    └── index.html        # JavaScript engine (rate fetching, caching, conversion)
```

---

## 🗺 Roadmap

- [x] v1.0 — Fiat + Crypto conversion with live rates
- [x] v1.0 — Offline cache with automatic failover
- [x] v1.0 — Multi-API redundancy
- [ ] v1.1 — Historical rate comparison ("USD to EUR last week")
- [ ] v1.2 — Multi-currency output ("100 USD in EUR, GBP, JPY")
- [ ] v2.0 — Portfolio tracking & alerts

---

## 🤝 Contributing

Contributions are welcome! Open a Pull Request or file an Issue on [GitHub](https://github.com/esvialv/exchange-converter).

---

<div align="center">
<sub>Built for offline Gemma-4-E4B-it inference on Google AI Edge Gallery · 100% private · No data leaves your device</sub>
</div>
