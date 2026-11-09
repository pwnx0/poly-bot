# Polyester Pro Trader (`poly-bot`) — v2.0 Community Edition

An automated trading, volume generation, and testnet reward engine for the **Polyester DEX Testnet**.

Built with TLS browser impersonation, automated SIWE authentication, deep liquidity anti-bleed guards, responsive maker limit orders, and realistic prop-trader circadian schedules.

---

## 🌟 What's New in v2.0 (Major Upgrade)

1. **🛡️ Deep Liquidity & Anti-Fund-Bleed Guard**:
   - Inspects 5 orderbook levels (`depth=2`) for bid/ask density.
   - Enforces minimum book depth ($\ge \max(\$1,500, 1.5 \times \text{size})$) and tight bid/ask ratio ($\ge 0.995$).
   - Strict **35 bps (0.35%) hard slippage cap** (replaces unsafe 5%–8% slippage), completely eliminating bad-fill fund bleeding on illiquid pairs.

2. **💎 60% Responsive Limit Order Maker Engine**:
   - Executes 60% of volume as resting limit orders at the top of the book, unlocking **maker fee discounts (>50% fee savings)**.
   - Uses a non-blocking 0.5s polling loop (up to 4.0s) to detect fills immediately without dead idle time.
   - **Instant Market Fallback**: If an order does not fill within 4s, it auto-cancels and fires an IOC market trade so volume velocity never halts.

3. **🎭 Organic Anti-Sybil Dynamic Sizing Engine**:
   - Replaces static order sizes with continuous organic percentage variance ($\pm 1.0\%$ to $\pm 2.2\%$) and random natural cents ($\pm \$1.50$).
   - Stateful consecutive separation ensures no two consecutive trades ever execute at the same or similar size ($> 1.5\%$ separation).
   - Dynamic portfolio scaling: set `TRADE_SIZE_USD=0` to auto-scale trade sizes with 15–20% of available wallet equity as faucet rewards accumulate.

4. **😴 Human Circadian Sleep Engine ($\pm 2\%$ Daily Variance)**:
   - Optional realistic human rest schedule (6–7 hours daily sleep).
   - Applies $\pm 2\%$ daily variation to sleep duration and bedtime to defeat robotic 24/7 Sybil detection.

5. **💧 Automatic Daily Faucet Claimer**:
   - Automatically checks and claims the $1,000 daily testnet faucet reward on startup and upon daily UTC resets.

6. **🔄 Multi-Asset Token Recycler**:
   - Automatically scans and liquidates airdropped or faucet tokens (SOL, AVAX, BNB, DOGE, HYPE, LTC, BCH, etc.) back to USDT/USDC to push volume and restore cash balances.

---

## ✨ Core Features

- **Automated SIWE Authentication**: Native Sign-In With Ethereum flow with instant smart-account resolution and local caching.
- **TLS Browser Impersonation**: Uses `curl_cffi` Chrome TLS fingerprints to prevent Cloudflare and API rate blocks.
- **Natural Order Flow**: Configurable discretionary holding delays (4.5s–9.0s) between order legs to simulate realistic human prop-trading.
- **Real-Time Telemetry & VIP Tracking**: Displays live session volume counters, round stats, and VIP tier tracking directly in your terminal.
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

# Pair to trade (e.g., SOL-USDT, BTC-USDT, ETH-USDT)
TRADING_PAIR=SOL-USDT

# Target order size in USD (Set to 0 for Dynamic Auto-Sizing 15-20% of balance)
TRADE_SIZE_USD=100.0

# Limit Order Maker Ratio (Default: 0.60 for 60% limit maker rounds)
LIMIT_ORDER_RATIO=0.60

# Enable Circadian Sleep Mode (6-7h human rest daily with +-2% variance)
ENABLE_HUMAN_SLEEP=false

# Auto-claim daily $1,000 testnet faucet
AUTO_CLAIM_FAUCET=true

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
| `SMART_ACCOUNT_ADDRESS` | *(Auto)* | Optional root Smart Account address (auto-detected if blank). |
| `TRADING_PAIR` | `SOL-USDT` | Spot market pair symbol on Polyester. |
| `TRADE_SIZE_USD`| `100.0` | Order size in USD per leg (set `0` for dynamic equity auto-sizing). |
| `LIMIT_ORDER_RATIO`| `0.60` | Proportion of rounds placed as resting limit orders (0.0 to 1.0). |
| `ENABLE_HUMAN_SLEEP`| `false` | Enable 6–7h daily sleep mode with $\pm 2\%$ daily jitter. |
| `AUTO_CLAIM_FAUCET`| `true` | Automatically claim daily $1,000 testnet faucet rewards. |
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
