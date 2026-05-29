# 🪙 MTG Coin Flip Simulator

A coin flip simulator inspired by *Magic: The Gathering* mechanics.

This project models probability using rule-based modifiers such as **Krark’s Thumb**, allowing users to simulate different flipping scenarios and track outcomes over time.

---

## 📸 Screenshots

### Full Application

![CoinFlip 1](static/CoinFlip1.png)

---

### Stats & History

<p align="center">
  <img src="static/CoinFlip2.png" width="48%" />
  <img src="static/CoinFlip3.png" width="48%" />
</p>

---

## 🎮 Features

- Flip a single coin
- Flip X coins (user-defined amount)
- Flip until first success (Heads)
- Flip until first failure (Tails)
- Krark’s Thumb mode (rule-modified probability system)
- Live tracking of:
  - Total Heads
  - Total Tails
  - Win Rate
- Flip history log (last 20 actions)
- Light / Dark mode toggle

---

## 🧠 Krark’s Thumb Rule

When enabled:
- Each coin flip is simulated twice
- The more favorable outcome is chosen

This creates a biased probability shift that can be observed over time.

---

## 🛠 Tech Stack

- SvelteKit
- TypeScript
- HTML / CSS
- JavaScript (`Math.random()` simulation)

---

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/coin-flip-simulator.git
cd coin-flip-simulator
npm install
npm run dev
