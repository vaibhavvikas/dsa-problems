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

### Solution:

```python
class Solution:
    def racecar(self, target: int) -> int:
        queue = deque([(0, 0, 1)])
        
        while queue:
            moves, pos, vel = queue.popleft()
            
            if pos == target:
                return moves
            
            # Always move forward
            queue.append((moves + 1, pos + vel, 2 * vel))
            
            # Backward only if car is ahead target, or you are
            # just in backward so you can simply hit backward
            # again to go pos
            if (pos + vel > target and vel > 0) or \
               (pos + vel < target and vel < 0):
                queue.append((moves + 1, pos, -vel//abs(vel)))
```
