# 🪙 MTG Coin Flip Simulator

An interactive probability simulator inspired by *Magic: The Gathering* mechanics.

The project models coin-flip outcomes using rule-based modifiers, including a simulation of **Krark’s Thumb**, and tracks results in real time.

---

## 🛠 Tech Stack

- SvelteKit  
- TypeScript  
- HTML / CSS  
- JavaScript  

---

## 📸 Preview

![CoinFlip 1](static/CoinFlip1.png)

---

## 🧠 Krark’s Thumb

<img src="static/krarks-thumb.jpg" width="220" />

When enabled, each coin flip is simulated twice and the more favorable outcome is selected. This modifies the underlying probability distribution compared to a standard 50/50 flip.

---

## 🎮 Features

- Single coin flip simulation  
- Batch coin flips (X flips)  
- Flip until success or failure  
- Krark’s Thumb mode (rule-based probability modifier)  
- Live statistics tracking:
  - Heads / Tails  
  - Win rate  
- Session history log  
- Light / Dark mode toggle  

---

## 📊 Project Focus

This project demonstrates:

- Probabilistic simulation modeling  
- Rule-based system design  
- Reactive state management in SvelteKit  
- Clean interactive UI architecture  
