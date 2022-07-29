120. Triangle

Given a triangle array, return the minimum path sum from top to bottom.

```python
Example:
triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
Output: 11
Explanation: The triangle looks like:
   "2"
  "3" 4
 6 "5" 7
4 "1" 8 3
The minimum path sum from top to bottom
2 + 3 + 5 + 1 = 11.
```
### Algorithm

#### Recursion + Memoization
```bash
We start from index[0][0]:

On each step we have two options:
either go left or right

our result is minimum of both situations
```
```
TC: O(n*m)
SC: O(n*m) + O(m) Aux Stack Space
```

#### Solution
```python
def minimumTotal(triangle):
    if len(triangle) == 1:
        return triangle[0][0]
    
    dp = [[None]*(i+1) for i in range(len(triangle))]
    dp[0][0] = triangle[0][0]
    
    def recurse(start, n, i):
        if start == n:
            return triangle[start-1][i]
        
        if dp[start][i] is not None:
            return dp[start][i]
        
        left = triangle[start-1][i] + recurse(start+1, n, i)
        right = triangle[start-1][i] + recurse(start+1, n, i+1)
        
        dp[start][i] = min(left, right)
        return dp[start][i]
    
    return recurse(1, len(triangle), 0)
```

#### Tabulation
```bash
Start from second last index
each index += min(bottom, bottom right)

return triangle[0][0]
```
```
TC: O(n*m)
SC: O(1) ~> Modifying the orig array
    O(n*m) ~> Create a dp array
    O(n) if space optimization
```

#### Solution
```python
def minimumTotal(triangle: List[List[int]]) -> int:
    for i in range(len(triangle)-2, -1, -1):
        for j in range(len(triangle[i])):
            triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1])
            
    return triangle[0][0]
```
