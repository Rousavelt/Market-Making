# High-Frequency Market Making Simulator & Microstructure Alpha Feed

A high-frequency quantitative trading framework built over a 48-hour research cycle using institutional-grade, tick-by-tick public market data from Tardis.dev. The project explores limit order book (LOB) dynamics, quantifies market price impact, and implements an inventory-controlled electronic market-making strategy on the Binance BTC-USDT pair.

## 📊 Core Architecture & Methodology

The simulator operates on a compressed **200-millisecond time slice interval** to align with the discrete broadcast intervals of the exchange matching engine, effectively handling network jitter and clock asynchrony.

### 1. High-Frequency Alpha Features Engineered
* **Net Toxicity Imbalance**: Measures the sequential momentum of informed, aggressive trade institutional blocks by separating true market execution fills from algorithmic cancellations.
* **Deep Order Book Imbalance (OBI)**: Evaluates the static structural support walls resting across the top 5 layers of the depth feed, mapping latent supply-and-demand pressure.
* **Kyle's Lambda ($\lambda$)**: Empirically estimates market tightness and asset price-sensitivity by measuring the real-time USD shift per unit of net aggressive Bitcoin volume traded.

### 2. Microstructure Backtesting Constraints Simulated
* **Price-Time Priority (FIFO Queue physics)**: Eliminates optimism bias by calculating a dynamic queue position tracker. Limit orders go to the back of the resting volume wall and decay proportionally alongside market cancellations and fills.
* **Zero Look-Ahead Enforcement**: Prevents chronological leaks by applying historical `.shift(1)` data lag operators on all indicator entry structures.
* **Non-Linear Inventory Control**: Implements an adaptive cubic exponential penalty scale ($q^3$) that alters toxicity and OBI barriers asymmetricly to maintain market neutrality.

## 📈 Performance Strategy Results Summary

* **Gross Day Trading PnL**: +$1,200 USD on 
* **Maximum Risk Exposure Ceiling**: 2.0 BTC (Peak Delta Risk exposure evaluated at roughly $4,000 USD against a $2,000 mean daily asset move. A draw down of approximately $160,000).
* **Mean Positional Balance**: -0.2 BTC (Confirming highly efficient gravitational convergence toward an inventory-neutral state).

## 🛠️ Tech Stack & Implementation
* **Language**: Python 3.11+
* **Core Libraries**: `pandas` (chunked data stream parsing), `numpy` (vectorized matrix computations), `matplotlib` (microstructural alpha scatter diagnostics).

## 🤖 AI Support: 
* Gemini, Claude, GPT5. A lot of the code itself was written by AI. My main focus was to:
* Download and process order book data
* Extract useful metrics for market makers, such as OBI, toxicity, and understand why these are useful.
* Create a simulator for backtesting a symbol algorithm using these metrics. Place/cancel orders depending on their values compared to some threshold. We ignore Kyle's lambda assuming our volumes are small enough not to impact the market.
* Dynamically adjust those thresholds to manage inventory risk, with more aggressive management the further we deviate from a desired threshold

## 🤷‍♂️ Caveats 
* We assume no transaction costs, this would probably annihilate our PnL
* We only place orders at the first level, never any deeper
* Our metrics are very out of date
* This wasn't written to be efficient, just as a learning tool for learning a bit more about market making
