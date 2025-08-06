
````markdown
# 📊 Crypto Analysis Automation with n8n

This repository contains a visual **crypto market analysis automation workflow** built with [n8n](https://n8n.io/). It collects multi-timeframe candlestick data for a selected crypto pair, analyzes the data using an AI agent, and delivers the result via Telegram and email.

---

## 🧠 Features

- ⏱️ Collects 15-minute, 1-hour, and 1-day candlestick data
- 🌍 Retrieves macro price sentiment using **Coindesk API**
- 📦 Combines multi-timeframe JSON data
- 🤖 Uses a Chat AI Agent (Google Gemini) to generate trading analysis
- 💬 Supports Telegram bot trigger and result delivery
- 📧 Sends email with detailed analysis
- 🛠 Built entirely in n8n (no external server needed)

---

## 🔁 Workflow Overview

```mermaid
graph LR
    A[Telegram Trigger] --> B{Format the Ticker}
    B --> C1[Get 15m Candle]
    B --> C2[Get 1h Candle]
    B --> C3[Get 1d Candle]
    C1 --> D[Merge Candles]
    C2 --> D
    C3 --> D
    D --> E[Combine JSON]
    E --> F1[Create Analysis (AI Agent)]
    F1 --> G1[Send to Email]
    F1 --> G2[Send to Telegram]
    B --> H[Coindesk API Request]
    H --> F1
````

---

## ⚙️ Nodes Used

### 1. **Trigger**

* **Telegram Trigger**: Starts the workflow when a message is received.

### 2. **Data Retrieval**

* `Get 15m Candle data`: HTTP request to fetch 15-minute candle data.
* `Get 1h Candle data`: HTTP request to fetch 1-hour candle data.
* `Get 1d Candle data`: HTTP request to fetch 1-day candle data.
* `Get Coindesk Data`: HTTP request to Coindesk API to retrieve BTC/USD historical and current data.

> Example Coindesk API Endpoint:
>
> ```
> https://api.coindesk.com/v1/bpi/currentprice/BTC.json
> ```

### 3. **Processing**

* `Format the ticker`: Formats ticker symbol from user input.
* `Merge & Combine JSON`: Merges all candle data and sentiment/macro data into unified JSON structure.

### 4. **AI Analysis**

* `Create The Analysis`: Uses a Gemini Chat Model to perform market analysis using candlestick and sentiment data.

### 5. **Output**

* `Send Email`: Sends a detailed trading recommendation.
* `Send Telegram Message`: Sends summarized analysis back to the user.

---

## 🧠 Analysis Breakdown

The AI Agent provides two types of recommendations:

* **Spot Trading**

  * Action (Buy, Sell, Hold)
  * Entry Price, Stop-Loss, Take Profit
  * Detailed rationale (price action, indicators, sentiment)

* **Leveraged Trading**

  * Position (Long/Short)
  * Leverage suggestion
  * Entry/Exit levels and full analysis

---

## 📬 How to Use

1. Clone this repo.
2. Import the workflow file into your n8n instance.
3. Configure:

   * Telegram credentials
   * API sources for candle data (Binance, Bybit, etc.)
   * Add **Coindesk API node** for macro sentiment
   * Google Gemini / AI credentials
   * Email SMTP config
4. Start the workflow and send a ticker like `BTCUSDT` via Telegram.

---

## 📁 File Structure

```bash
📦crypto-analysis-n8n
 ┣ 📜README.md
 ┗ 📜workflow.json (optional if exporting the workflow)
```

---

## 🧩 Dependencies

* n8n v1+
* Telegram Bot
* Access to candlestick data API (e.g., Binance, Bybit)
* Coindesk API (Free, no auth required)
* Google Gemini AI Key
* SMTP for Email

---

## 🛡️ License

MIT License. Feel free to use and modify.

---

## 🤝 Contributions

Pull requests are welcome. Let's make automated crypto analysis more accessible 🚀




