## Longest Common Substring

You have been given two strings 'STR1' and 'STR2'. You have to find the length of the longest common substring.
A string “s1” is a substring of another string “s2” if “s2” contains the same characters as in “s1”, in the same order and in continuous fashion also.

### Algorithm

```bash
if two elements match then we check if:
previous also matched.

if matched then 1 + len_prev_matched
else: 1

any other case we keep it as 0
```

### Solution

```python
def lcs(str1, str2):
    dp = [[0]*(len(str2)+1) for _ in range(len(str1)+1)]
    max_len = 0

    for i in range(1, len(str1)+1):
        for j in range(1, len(str2)+1):
            if str1[i-1] == str2[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
                max_len = max(max_len, dp[i][j])
    
    return max_len
```
