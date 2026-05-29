# 🪙 MTG Coin Flip Simulator

An interactive probability simulation tool inspired by *Magic: The Gathering* mechanics.  
This project explores rule-modified randomness using coin-flip simulations, including mechanics such as **Krark’s Thumb**, and provides real-time tracking of outcomes, statistics, and session history.

---

## 📸 Preview

### 🖥️ Full Interface
A clean overview of the full application layout in its default state.

![CoinFlip 1](CoinFlip1.png)

---

### 🌙 Dark Mode + Live Statistics
Displays real-time tracking of heads, tails, and win rate with Krark’s Thumb enabled.

![CoinFlip 2](CoinFlip2.png)

---

### ☀️ Light Mode + History Log
Shows session history and flip tracking in light mode for readability comparison.

![CoinFlip 3](CoinFlip3.png)

---

## 🎮 Core Features

- Flip a single coin with simulated randomness
- Flip X coins (user-defined batch simulation)
- Flip until first success (Heads)
- Flip until first failure (Tails)
- Krark’s Thumb mode (rule-modified probability system)
- Real-time statistics tracking:
  - Total Heads
  - Total Tails
  - Win Rate
- Session history log (last 20 actions)
- Light / Dark mode toggle

---

## 🧠 Krark’s Thumb Mechanics

When enabled, coin flips are modified as follows:

- Each flip is simulated twice
- The more favorable outcome is selected

This creates a biased probability distribution that diverges from standard 50/50 randomness over time, allowing users to observe long-term statistical effects.

---

## 🛠 Tech Stack

- SvelteKit
- TypeScript
- HTML / CSS (custom styling)
- JavaScript (`Math.random()` based simulation logic)

---

## 📊 Project Goals

This project was built to demonstrate:

- Probabilistic simulation modeling
- Rule-based modification of randomness
- Reactive UI state management in SvelteKit
- Clean UI structuring and user interaction design

---

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/mtg-coin-flip-simulator.git
cd mtg-coin-flip-simulator
npm install
npm run dev
