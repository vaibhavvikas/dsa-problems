## 13. Roman to Integer

```
TC: O(n) ~> n is len of string
SC: O(1) No extra Space
```
### Solution

```python
def romanToInt(self, s: str) -> int:
    romans = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000,
                'IV': 4,'IX': 9, 'XL': 40, 'XC': 90, 'CD': 400, 'CM': 900}
    
    i, n, res = 0, len(s), 0
    
    while True:
        if i >= n:
            break
            
        if i + 1 < n and s[i]+s[i+1] in romans:
            res += romans[s[i]+s[i+1]]
            i += 2
        else:
            res += romans[s[i]]
            i += 1
            
    return res
```