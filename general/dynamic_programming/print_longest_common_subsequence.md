## Print Longest Common Subsequence

**Extension of [Longest Common Subsequence](./longest_common_subsequence.html)**

### Algorithm:

```bash
First form the tabulation:
s = adebc and t = dcadb
      d  c  a  d  b
 [[0, 0, 0, 0, 0, 0],
a [0, 0, 0, 1, 1, 1],
d [0, 1, 1, 1, 2, 2],
e [0, 1, 1, 1, 2, 2],
b [0, 1, 1, 1, 2, 3],
c [0, 1, 2, 2, 2, 3]]

Take two indexes 

i = len(s), j = len(t)

start from end:
Case 1:
    if both equal add it to res and
    decrement both
Case 2:
    check the max of left and top
    of both and move accordingly.
```

### Solution

```python
def print_lcs(s, t) :
    s_length, t_length = len(s), len(t)
    
    dp = [[0]*(t_length+1) for _ in range(s_length+1)]
    
    for i in range(1, s_length+1):
        for j in range(1, t_length+1):
            if s[i-1] == t[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
                
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    

    res = [None for _ in range(dp[-1][-1])]
    i, j = s_length, t_length
    res_ind = -1

    while i > 0 and j > 0:
        if s[i-1] == t[j-1]:
            res[res_ind] = s[i-1]
            res_ind -= 1
            i -= 1
            j -= 1
        else:
            if dp[i][j-1] > dp[i-1][j]:
                j -= 1
            else:
                i -= 1

    return "".join(res)
```