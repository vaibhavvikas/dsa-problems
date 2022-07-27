## Min insertions to make a string palindrome

Given a string find minimum number of insertions to make a string palindrome

for e.g. String s = “abcaa” can be converted into a palindrome by inserting 2 characters. So the final string becomes “aabcbaa”.

### Algortihm
```python
Step 1: Using palindrome to find max length
    of the palindrome
    i.e. compare string and its reverse.

Step 2: 
    lets take a str, "abcdea"
    max len pali: a c a
    so palindrome will "a b |ed| c de |b| a"

Step 3: Looking we clearly see that
    the number of strings will be:
    len(str) - len(max_pali)
```
```bash
TC ~> O(n^2)
SC ~> O(n^2)
```

### Solution

```python
def min_ins(s);
    t = s[::-1]
    n = len(s)

    dp = [[0]*(n+1) for _ in range(n+1)]

    for i in range(1, n+1):
        for j in range(1, n+1):
            if s[i-1] == t[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return n - dp[-1][-1]
```