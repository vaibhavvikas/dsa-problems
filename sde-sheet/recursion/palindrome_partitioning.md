## Palindrome Partitioning

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

```bash
Example:
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

### DFS Approach
```
We start from ind = 0 and 
make a partiton using the
loop each time we can make
a palindrome.
```
```bash
TC: O((2^n) *k*(n/2))
SC: O(k*x)
k is avg length of pali
and x such list of pali
```

### Solution
```python
def partition(self, s: str):
    res = []
    n = len(s)
    
    def is_pali(string):
        for i in range(len(string)//2):
            if string[i] != string[~i]:
                return False        
        return True
    
    def helper(ind, curr):
        if ind == n:
            res.append(curr)
            return
            
        for i in range(ind, n):
            if is_pali(s[ind:i+1]):
                helper(i+1, curr + [s[ind:i+1]])
                
    helper(0, [])
    return res
```