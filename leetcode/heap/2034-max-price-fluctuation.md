## 2034. Stock Price Fluctuation

**Given:**

Stream of records: [timestamp, price]
Records are not in order and worse soem price may come wrong,
so at later we can get the same timestamp with different price.

**Objective:**

Algorithm with these functionalities:

```python
# Initializes the object with no price records.
StockPrice()

# Updates the price of the stock at the given timestamp.
void update(int timestamp, int price) 

int current() # Returns the latest price of the stock.
int maximum() # Returns the maximum price of the stock.
int minimum() # Returns the minimum price of the stock.
```

### Algorithm

```python
1. We use heap to get the maximum and minimum price
   in least amount of time
```
```python
TC: O(logn) for find max or min, for rest its O(1)
SC: O(n)
```


### Solution

```python
class StockPrice:

    def __init__(self):
        self.stock = {}
        self.largest = []
        self.smallest = []
        self.most_recent = -math.inf
        

    def update(self, timestamp: int, price: int) -> None:
        self.stock[timestamp] = price
        self.most_recent = max(self.most_recent, timestamp)
        heapq.heappush(self.largest, (-price, timestamp))
        heapq.heappush(self.smallest, (price, timestamp))

    def current(self) -> int:
        return self.stock[self.most_recent]

    def maximum(self) -> int:
        while self.stock[self.largest[0][1]] != -self.largest[0][0]:
            heapq.heappop(self.largest)
        return -self.largest[0][0]

    def minimum(self) -> int:
        while self.stock[self.smallest[0][1]] != self.smallest[0][0]:
            heapq.heappop(self.smallest)
        return self.smallest[0][0]
```