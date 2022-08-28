## 84. Largest Rectangle in Histogram

Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

```bash
Example:
Input: heights = [2,1,5,6,2,3]
Output: 10

      x
    v v
    v v
    v v   x
x   v v x x
x x v v x x
```

### Stack Approach:
```bash
For each element we need two things
net smallest from left and next
smallest from right. Which together
will make the width of the rectangle

So to do this we are using stack:

Step 1. Next smallest from left
we initialize the array with -1

for the first index the next smallest is
index 0
we put 0 in index

now for each element if the stack top
is greater than current we pop the stack

at last if stack has something, nsl is
the top index

other wise it has no smallest from left
i.e -1

Step 2. Next smallest from right
we use the same approach and initialize
nsr with n as the elemnt

use same steps as above

Step 3.
The width is nsr[i] - nsl[i] - 1
We use this and the hright as curr and
find max area
```
```
TC: O(n)
SC: O(n)
```

### Solution
```python
def largestRectangleArea(self, heights: List[int]) -> int:
    n = len(heights)
    
    nsl = [-1 for _ in range(n)]
    stack = [0]
    
    for idx in range(1, n):
        curr = idx
        while stack and heights[stack[-1]] >= heights[idx]:
            stack.pop()
        if stack:
            nsl[idx] = stack[-1]
        stack.append(idx)
        
    nsr = [n for _ in range(n)]
    stack = [n-1]
    
    for idx in range(n-2, -1, -1):
        curr = idx
        while stack and heights[stack[-1]] >= heights[idx]:
            stack.pop()
        if stack:
            nsr[idx] = stack[-1]
        stack.append(idx)
    
    res = 0
    
    for i in range(n):
        width = nsr[i] - nsl[i] - 1
        res = max(res, width*heights[i])
        
    return res
```

### Stack One - Pass

```bash
For each step,
in the case the current element is less
than stack top then we know the nsr is
the current index

We assign the current height as stack[top]
and pop it

Now we have two cases, if stack is empty
that means the nsl is -1 else nsl is the 
top of stack.

We use these to calculate area and keep
doing this till we reach end of stack
```
```bash
TC: O(n)
SC: O(n)
```

### Solution

```python
def largestRectangleArea(heights):
    n = len(heights)
    stack = []
    res = 0
    
    for i in range(0, n+1):
        while stack and (i == n or heights[stack[-1]] >= heights[i]):
            height = heights[stack[-1]]
            stack.pop()
            
            width = i
            if stack:
                width = i - stack[-1] - 1
    
            res = max(res, width*height)
        
        stack.append(i)
        
    return res
```
