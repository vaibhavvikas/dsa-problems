## 12. Integer to Roman

```bash
TC: O(1)
SC: O(1)
```

```python
def intToRoman(self, num: int) -> str:
    roman_map = [("M", 1000), ("CM", 900), ("D", 500),
                    ("CD", 400), ("C", 100), ("XC", 90),
                    ("L", 50), ("XL", 40), ("X", 10),
                    ("IX", 9), ("V", 5), ("IV", 4),
                    ("I", 1)]
    
    res = ""
    for each in roman_map:
        res += (num//each[1]) * each[0]
        num -= (num//each[1]) * each[1]
    
    return res
```