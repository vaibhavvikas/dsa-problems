## 146. LRU Cache

Design and implement a data structure for a Least Recenty Used (LRU) cache.

### Algorithm
```bash
Step 1. Create Ordered Dict
Step 2. Get Functions:
    If the item is not there return -1
    else:
        move the element to end
        and return its value
Step 3. Put Function:
    If item is there, update it
    Move it to end
    If length exceeds remove the
    first element
```
```
TC: Get ~> O(1), Put ~> O(1)
SC: O(n)
```


### Solution

```python
class LRUCache:
    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]        

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```