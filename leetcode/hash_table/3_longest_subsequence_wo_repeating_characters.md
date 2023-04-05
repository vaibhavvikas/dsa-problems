### 3. Longest Substring Without Repeating Characters

```python
def lengthOfLongestSubstring(self, s: str) -> int:
    left, right, res = 0, 0, 0
    char_set = set()
    
    for right in range(len(s)):
        if s[right] in char_set:
            while left < right and s[right] in char_set:
                char_set.remove(s[left])
                left += 1
                
        char_set.add(s[right])
        res = max(res, right-left+1)
    
    return res
```
