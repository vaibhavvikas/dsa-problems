## 85. Maximal Rectangle
Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

 ```bash
 Example:
 Input: [["1","0","1","0","0"],
         ["1","0","1","1","1"],
         ["1","1","1","1","1"],
         ["1","0","0","1","0"]]
Output: 6
```

### Histogram algorithm
```Bash
We use the histogram approach
For each step we have 
if we get zero we make histogram 0
else we add 1 to curr

and then call the histogram func
to find the area
```
```
TC: O(m*n) + O(n)
SC: O(n)
```

### Solution
```python
def maximalRectangle(matrix):
    m, n = len(matrix), len(matrix[0])
    
    def find_max_area(hist):
        stack = []
        area = 0
        for i in range(n+1):
            while stack and (i == n or hist[stack[-1]] >= hist[i]):
                height = hist[stack[-1]]
                stack.pop()
                
                width = i
                if stack:
                    width = i - stack[-1] - 1
                
                area = max(area, width*height)
                
            stack.append(i)
            
        return area
    
    res = 0
    
    curr = [0]*n
    for i in range(m):
        for j in range(n):
            if matrix[i][j] == "0":
                curr[j] = 0
            else:
                curr[j] += 1
        res = max(res, find_max_area(curr))
        
    return res
```