# 🧾 Order Types Overview

An order can be one of the following types:

- Market  
- Limit  
- Stop Market  
- Stop Limit  
- OCO (One-Cancels-the-Other)

---

## 🟢 Market Order

A market order is executed at the current market price.  
This means the buyer or seller wants to buy or sell immediately at the best available price.

### Example Parameters:
```text
Side: BUY  
Symbol: BTC-USDT  
Quantity: 0.001
```

- `Side` specifies the direction of the order: either BUY or SELL.
- `Symbol` defines the trading pair, e.g., BTC-USDT.
- `Quantity` is a portion of the base asset. It must be expressed in base units for both buy and sell orders.

📌 The above order means: Buy 0.001 BTC at market price.

Market orders are not placed in the order book.

After parameter validation, the matching engine executes the trade against the best available price in the order book.

---

## 🟠 Limit Order

Unlike market orders, limit orders are executed at a specified price. The trader sets a price at which they want to buy or sell. This helps prevent price slippage, as the order is placed in the order book and will only be filled at the specified price.

### Example Parameters:

```text
Side: SELL  
Type: LIMIT  
Symbol: ADA-USDT  
Quantity: 30  
Price: 0.934
```

- Price is the trader’s specified price.

Once validated, the order enters the order book. Two scenarios may occur:

- If a matching order at the same price exists, the trade is executed.
- If not, the order waits in the book until a matching counter-order arrives.

---

## 🔵 Stop Market Order
Stop orders allow traders to interact with the market conditionally. A Stop Market order is triggered when the price reaches a specific level.

### Example Parameters:
```text
Side: BUY  
Type: STOP_MARKET  
Symbol: BTC-USDT  
Quantity: 0.0025  
Stop Price: 116173.87
```
📌 Translation:

> When BTC price reaches 116173.87, buy 0.0025 BTC at market price.

---

## 🟣 Stop Limit Order
Stop Limit orders offer more control and are useful for algorithmic or strategic trading. They behave like Stop Market orders but place a Limit order once the stop price is reached.

This type of order enters the order book and behaves like a regular Limit order, but only after being triggered.

### Example Parameters:

```text
Side: SELL  
Type: STOP_LIMIT  
Symbol: ADA-USDT  
Quantity: 30  
Stop Price: 0.934  
Price: 0.91
```

📌 Translation:

> When ADA price reaches 0.934, place a Limit sell order for 30 ADA at 0.91.

---

## 🟡 OCO Order (One-Cancels-the-Other)

An OCO order combines two conditional orders (Limit or Stop Limit). Only one of them can be executed. Once one is filled, the other is automatically canceled.

This type of order is ideal for:

- Locking in profits (Take Profit) while limiting losses (Stop Loss)
- Entering the market at two different levels (e.g., breakout above resistance or drop below support)

---

## 📊 Order Type Comparison

| Order Type     | Price Specified | Enters Order Book | Trigger Condition        |
|----------------|------------------|--------------------|------------------------|
| Market         | ❌               | ❌                 | Immediate              |
| Limit          | ✅               | ✅                 | Price match            |
| Stop Market    | ❌               | ❌                 | Stop price             |
| Stop Limit     | ✅               | ✅                 | Stop price             |
| OCO            | ✅ / ✅          | ✅                 | One fills, one cancels |

## 🔁 Order Flow Diagram

```text
User → Submit Order → Validate →
  ├─ Market → Match Immediately
  ├─ Limit → Add to Order Book → Wait for Match
  ├─ Stop Market → Wait for Trigger → Match at Market Price
  ├─ Stop Limit → Wait for Trigger → Add Limit to Order Book
  └─ OCO → Submit Two Orders → One Executes → Other Cancels
```


## ⚡ Trade Execution Condition

For the matching engine to execute a trade, the following condition must be met:

```text
Bids.top.price >= Asks.top.price
```

This means the highest bid must be greater than or equal to the lowest ask. Only then will the matching engine pair buy and sell orders to complete a trade.

> Entering an order into the order book does not guarantee execution. A trade occurs only when the best buy and sell prices overlap.

