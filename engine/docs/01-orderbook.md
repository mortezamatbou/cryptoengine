# 📘 What Is an Order Book?

An order book is a real-time list of active buy and sell orders placed by traders in the market.

The list of buy/sell requests in the order book changes dynamically based on supply and demand. This can happen when:
- A new buy or sell order is placed by a user.
- An existing order in the order book is canceled by the user.
- The matching engine matches an order and a trade is executed, triggering an update to the order book.

---

## 💱 Currency Pair

A currency pair like `BTC-USDT` consists of two parts:
- **Base**: BTC
- **Quote**: USDT

### 🔄 A Trade Has Two Sides:
- **Buy**
- **Sell**

In a trade:
- The buyer receives the **Base** asset.
- The seller receives the **Quote** asset.

---

## 🧾 Basic Order Structure

An order typically includes:
- `Side` → BUY or SELL  
- `Type` → Limit or Market  
- `Amount` → A multiple of the base unit  
- `Pair` → e.g., BTC-USDT  
- `Price` → Desired price for buying or selling

### 🛠️ Order Types
- **Limit**: Executes at a specified price or better.
- **Market**: Executes immediately at the current market price.

> ℹ️ Only limit orders are added to the order book.  
> Market orders are processed immediately upon reaching the matching engine, indicating the user wants to trade at the current market price.

---

## 🔁 Order Flow: From Submission to Order Book

User `C1` wants to sell `0.001 BTC` at a price of `115852.35` in the `BTC-USDT` market.  
Assuming the user places a limit order, the order details are:

- `Side` → SELL  
- `Type` → Limit  
- `Amount` → 0.001  
- `Pair` → BTC-USDT  
- `Price` → 115852.35

After validation and policy checks by the matching engine (to be discussed later), and assuming the order is valid, it is added to the order book.

---

## 🧩 Taker vs. Maker Orders

When an order is placed (regardless of buy or sell), if it is immediately filled by an existing order in the order book, it is considered a **Taker** order.

If the order remains in the order book and is filled later by another incoming order, it is considered a **Maker** order.

> ✅ If your order is filled by others → You are a **Maker**  
> ❌ If your order fills others immediately → You are a **Taker**

---

## 📊 Order Book Structure

The order book consists of two main sections:
- **Asks** → Sell offers
- **Bids** → Buy offers

Each order in the book includes:
- **Price**
- **Volume**

### 🧮 Example Orders

```text
2025-08-13 14:23:25 → User C1 places a sell order for 0.001 BTC at 114578.32  
2025-08-13 14:23:26 → User C2 places a buy order for 0.005 BTC at 114889  
2025-08-13 14:24:01 → User C3 places a buy order for 0.047 BTC at 114889.1  
2025-08-13 14:24:05 → User C4 places a sell order for 0.061 BTC at 114578.32  
2025-08-13 14:24:06 → User C5 places a buy order for 0.001 BTC at 114578.32
```

After validation, these orders are added to the order book and it is updated accordingly.

These orders represent supply and demand in the market. Based on the sell orders from C1 and C4 at the same price, we now have:

> `0.001 + 0.061 = 0.062 BTC` available for sale at `114578.32`

---

## 📐 Sorting Bids and Asks

- **Asks** (sell orders) are sorted in ascending order → from lowest to highest price.
- **Bids** (buy orders) are sorted in descending order → from highest to lowest price.


## 🔍 Key Terms

- `asks.top` → First row in asks (lowest sell price)

- `bids.top` → First row in bids (highest buy price)

- `asks.top.price` → Current lowest sell price

- `bids.top.price` → Current highest buy price

## ⚡ Matching Condition

When the following condition is met:

```text
asks.top.price <= bids.top.price
```

The matching engine begins matching orders, and trades are executed between buyers and sellers.