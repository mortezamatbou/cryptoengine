# 🧮 Crypto Matching Engine Simulation

This repository is designed to simulate a matching engine, an order book, and real-time order simulation for the cryptocurrency market. The focus is on the **spot market**.

## ⚙️ Engine Capabilities

The trading engine supports:
- **Market**
- **Limit**
- **Stop-market**
- **Stop-limit**
- **OCO** orders

Limit orders can be configured with:
- `IOC` (Immediate or Cancel)
- `FOK` (Fill or Kill)
- `GTC` (Good Till Cancelled)
- `post-only`

Each option serves a specific purpose for trader interaction.

## 🐳 Dockerized Architecture

The project is fully dockerized and includes the following containers:
- `db`: TimescaleDB for time-series optimized PostgreSQL
- `redis`: For caching and event streaming
- `engine`: C++ matching engine

### 🧾 CLI Container Capabilities

The `cli` container can:
- Add users to the system
- Place orders for users
- Create markets (e.g., BTC-USDT)
- Activate/deactivate markets for order placement
- Written in **python**

## 🗃️ Database & Caching

- **TimescaleDB** is used to store and retrieve time-series data like candles and ticks.
- **Redis** is used for:
  - Caching order book data
  - Redis Streams for event-driven architecture, allowing the engine to react instantly to new orders

## 🚀 Matching Engine Details

- Written in **C++**
- Located in the `engine` container
- Implements **FIFO** with **price-time priority**
- Ensures fair order fulfillment, especially important for retail traders
- Inspired by algorithms used in major exchanges

## 🔬 Project Scope

This is a **research project** and a **toy version** of a matching engine.
It is **not recommended for production use** and requires:
- Extensive testing
- Deep understanding of the codebase

Feel free to:
- Submit pull requests
- Fork the project
- Treat it as your own

## 📚 Documentation

Each container includes a `docs` folder with markdown files documenting:
- Component functionality
- Design details
This helps maintain organized and accessible documentation.

## 🙏 Final Notes

Apologies for any grammatical mistakes in commits or markdowns.
I hope this repository serves as a starting point for those curious about building a matching engine for a crypto exchange and helps them grasp the core concepts.

> The longest journeys begin with small steps, and the destination is not the end.

### 💡 Coding Philosophy

Beyond Clean Code, SOLID principles, and Design Patterns, I always keep these in mind:

- Keep it simple
- Less is more
- Take small steps, every day (Kaizen)
- Good software, like wine, takes time

The best software or products often start with the most basic versions.
With consistent development, they evolve into best practices.

### 🧠 Quotes That Matter

> Do one thing and do it well. (Unix Philosophy)

> What I cannot create, I do not understand. (Richard Feynman)

---

I'm happy to share this repository with you.  
If it benefits even one person in the world, then I've achieved my goal.

**Best regards**
**Morteza Matbou**
Founder of Lobdown
August 12, 2025
