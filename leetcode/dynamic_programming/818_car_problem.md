## 818: Car Problem

**Given:**
Your car starts at position 0 and speed +1 on an infinite number line.
Car can do two things Accelerate (A) or Reverse (R)
Car can go into negative positions.

```bash
Condition A:
    position += speed
    speed *= 2

Condition R:
    if curr_speed > 0: speed = -1
    else: speed = 1 
```
```
For example, after commands "AAR", 
car goes to positions 0 --> 1 --> 3 --> 3,
and speed goes to 1 --> 2 --> 4 --> -1.
```

**Objective:**
Find minimum moves to reach the destination.

### Dijkstra's Algorithm
```
TC: O(nlogn)
SC: O(n)
```
### Solution:

```python
def racecar(target: int) -> int:
    pqueue = [(0, 0, 1)]
    
    while pqueue:
        moves, pos, vel = heapq.heappop(pqueue)
        
        if pos == target:
            return moves
        
        # Always move forward
        heapq.heappush(pqueue, (moves + 1, pos + vel, 2 * vel))
        
        # Backward only if car is ahead target, or you are
        # just in backward so you can simply hit backward
        # again to go pos
        if (pos + vel > target and vel > 0) or \
            (pos + vel < target and vel < 0):
            heapq.heappush(pqueue, (moves + 1, pos, -vel//abs(vel)))
```
