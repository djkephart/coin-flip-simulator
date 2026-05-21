# MTG Coin Flip Simulator

A coin flip simulator intended for Magic: The Gathering mechanics.

This project models coin flip probability with rule-based modifiers inspired by MTG cards such as **Krark’s Thumb**, allowing users to simulate different flipping scenarios and track outcomes over time.

---

## 🎮 Features

- Flip a single coin
- Flip X coins (user-defined amount)
- Flip until first failure (Tails)
- Flip until first success (Heads)
- Krark’s Thumb mode (modifies coin outcomes)
- Live tracking of:
  - Total Heads
  - Total Tails
  - Win rate
- Flip history log
- Light/Dark mode toggle

---

## 🧠 Krark’s Thumb Rule

When enabled:
- Each coin flip is replaced with two flips
- The favorable result is chosen (increases probability of success)

---

## 🛠 Tech Stack

- SvelteKit
- TypeScript
- HTML / CSS (custom styling)
- JavaScript Math.random() for simulation

---

## 🚀 Getting Started

Clone the repo:

```bash
git clone https://github.com/your-username/mtg-coin-flip-simulator.git
cd mtg-coin-flip-simulator
