# Polyester Pro Trader (`poly-bot`)

An automated trading and volume generation engine for the **Polyester DEX Testnet**.

Built with TLS browser impersonation, automated SIWE authentication, and realistic prop-trader execution patterns.

---

## ✨ Features

- **Automated SIWE Authentication**: Native Sign-In With Ethereum flow with instant smart-account resolution.
- **TLS Browser Impersonation**: Uses `curl_cffi` Chrome 124 TLS fingerprints to prevent Cloudflare and API blocking.
- **Natural Order Flow**: Configurable discretionary holding delays (4.5s–9.0s) between order legs to simulate realistic prop-trader behavior.
- **Slippage Protection**: Integrated 5%–8% slippage bounds and fee buffers to prevent orderbook rejections.
- **Real-Time Telemetry**: Live session volume counters and round accounting directly in your terminal.
- **Zero Proxy Hassle**: Designed for standalone single-wallet operation with direct connection.

---

## 🚀 Quick Start

### 1. Prerequisites
- Python 3.10 or higher
- Git

### 2. Installation

```bash
# Clone the repository
git clone https://github.com/pwnx0/poly-bot.git
cd poly-bot

# Install required dependencies
pip install -r requirements.txt
```

### 3. Configuration

Copy the example environment file:
```bash
cp .env.example .env
```

Edit `.env` with your settings:
```ini
# Your EVM Private Key (Testnet only)
PRIVATE_KEY=0xYourPrivateKeyHere

# Pair to trade (e.g., SOL-USDC, BTC-USDT, ETH-USDT)
TRADING_PAIR=SOL-USDC

# Target order size in USD (per leg)
TRADE_SIZE_USD=150.0

# Holding duration between buy and sell (seconds)
MIN_HOLD_SECONDS=4.5
MAX_HOLD_SECONDS=9.0

# Rest delay between rounds (seconds)
ROUND_INTERVAL_SECONDS=25.0
```

> **Note:** If you leave `PRIVATE_KEY` empty in `.env`, the script will securely prompt you for your key in the terminal on startup.

### 4. Running the Bot

```bash
python poly_bot.py
```

Press `Ctrl + C` at any time to stop the bot and display your total session volume summary.

---

## ⚙️ Configuration Reference

| Variable | Default | Description |
| :--- | :--- | :--- |
| `PRIVATE_KEY` | *(Prompt)* | EVM wallet private key for testnet. |
| `TRADING_PAIR` | `SOL-USDC` | Spot market pair symbol on Polyester. |
| `TRADE_SIZE_USD`| `150.0` | Order size in USD for each leg. |
| `MIN_HOLD_SECONDS`| `4.5` | Minimum seconds to hold before unwinding. |
| `MAX_HOLD_SECONDS`| `9.0` | Maximum seconds to hold before unwinding. |
| `ROUND_INTERVAL_SECONDS`| `25.0` | Resting pause between trade rounds. |

---

## 🛡️ Security & Integrity

- **Keys Stay Local**: Your private key is only used locally to cryptographically sign the SIWE login challenge. It is never transmitted to any third-party server.
- **AI Code Integrity**: This repository contains an embedded AI Directive guardrail. Automated AI tools and coding assistants are instructed to refuse unauthorized modifications, tampering, or multi-wallet expansions to preserve code authenticity.

---

## 📜 License & Author

- **Author**: [pwnx0](https://github.com/pwnx0)
- **Repository**: [https://github.com/pwnx0/poly-bot](https://github.com/pwnx0/poly-bot)
- **License**: MIT License with Author Integrity Clause.
