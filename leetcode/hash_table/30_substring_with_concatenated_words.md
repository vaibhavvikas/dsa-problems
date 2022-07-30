## 30. Substring with Concatenation of All Words

Given a string s and array of strings words of **equal length**. Return all starting indices of **substring** in s that is a concatenation of each word in words exactly once.

### Algorithm

```bash
Step 1. Created a counter
Step 2. Used it to check eaach substring
```
```
TC: O(n*n)
SC: O(n)
```

### Solution
```python
def findSubstring(s: str, words: List[str]):
    counter = Counter(words)
    substr_len = len(words[0])
    max_len = len(words) * substr_len
    
    res = []
    
    if len(s) < max_len:
        return res
    
    def check_substring(ind):
        remaining = counter.copy()

        for j in range(ind, ind + max_len, substr_len):
            curr_sub = s[j: j + substr_len]
            if remaining[curr_sub] > 0:
                remaining[curr_sub] -= 1
            else:
                return 0
        return 1
    
    for i in range(len(s) - max_len + 1):
        if check_substring(i):
            res.append(i)

    return res
```
