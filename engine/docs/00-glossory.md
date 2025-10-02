# 📖 Order Book Glossary

This glossary defines key terms used in the structure and behavior of an order book.

---

### `Asks`
List of sell orders in the order book.

### `Bids`
List of buy orders in the order book.

### `Asks.top`
The lowest sell offer in the order book.

### `Bids.top`
The highest buy offer in the order book.

### `Bids.top.price`
The highest bid price currently in the order book.

### `Asks.top.price`
The lowest ask price currently in the order book.

### `Asks.top.amount`
The total amount available for sale at the lowest ask price.

### `Bids.top.amount`
The total amount available for purchase at the highest bid price.

---

### `Asks[i]`
The i-th row in the list of sell offers.  
Index `i` starts from 1.  
Sell orders are sorted in ascending order by price.  
Therefore, `Asks.top` is equivalent to `Asks[1]`.

### `Bids[i]`
The i-th row in the list of buy offers.  
Index `i` starts from 1.  
Buy orders are sorted in descending order by price.  
Therefore, `Bids.top` is equivalent to `Bids[1]`.

### `Asks[i].price`
The ask price at the i-th row of the order book.

### `Bids[i].price`
The bid price at the i-th row of the order book.

### `Bids[i].amount`
The available buy volume at the i-th row of the order book.

### `Asks[i].amount`
The available sell volume at the i-th row of the order book.

---

### `Spread`
The price difference between the highest bid and the lowest ask.  
Calculated as:  
`Spread = Bids.top.price - Asks.top.price`

### `MidPrice`
The average of the highest bid and the lowest ask.  
Calculated as:  
`MidPrice = (Bids.top.price + Asks.top.price) / 2`
