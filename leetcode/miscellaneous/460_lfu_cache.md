## LFU Cache

Design and implement a data structure for a Least Frequently Used (LFU) cache.

### Algorithm
```bash
Step 1. Create a dict for cache
    Create a defaultdict orderedDict
    for usage

    Each item has 3 values.
    Its key, Its value, its freq
    So we create an obj and say it Node

Step 2. Get Function
    If item is not there return -1
    If its there We need to update its freq
    and return it

Step 3. Put Func
    If the item is not there, we need to add it

    Check if size reaached max:
    from usage -> min_freq -> remove first
    usage[minfreq] -> pop_first_item

    Create a new entry and put it with freq 1
    set self.min_freq as 1

    If its there -> update it

Step 4. Update Function
    We get its key and value
    and update its value
    get its freq

    Check usage -> its freq and remove it
    if freq is empty after removing
    also remove the freq key
    and check if it was the min freq if yeah
    increment min_freq by 1

    Now, update node frequency by 1
    usage -> self.freq + 1 -> key -> value

```
```bash
TC: Get ~> O(1), Put ~> O(1)
SC: O(n) + O(n)
```

## Solution

```python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.freq = 1

class LFUCache:
    def __init__(self, capacity: int):
        self.cache = {}
        self.usage = defaultdict(OrderedDict)
        self.min_freq = 0
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        node = self.cache[key]
        self.update(node)
        return node.value

    def put(self, key: int, value: int) -> None:
        if self.capacity == 0:
            return
        
        if key not in self.cache:
            if len(self.cache) >= self.capacity:
                k, _ = self.usage[self.min_freq].popitem(last=False)
                self.cache.pop(k)
            node = Node(key, value)
            self.cache[key] = node
            self.usage[1][key] = value
            self.min_freq = 1
        else:
            node = self.cache[key]
            node.value = value
            self.update(node)
                
    def update(self, node):
        k, f = node.key, node.freq
        self.usage[f].pop(k)
        if not self.usage[f] and self.min_freq == f:
            self.min_freq += 1

        self.usage[f+1][k] = node.value
        node.freq += 1
```