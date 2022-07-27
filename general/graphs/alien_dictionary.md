## Alien Dictionary

Given a sorted dictionary of an alien language having N words and k starting alphabets of standard dictionary. Find the order of characters in the alien language.
Note: Many orders may be possible for a particular test case, thus you may return any valid order and output will be 1 if the order of string returned by the function is correct else 0 denoting incorrect string returned.

### Algorithm
```bash
Example: {"baa","abcd","abca","cab","cad"}

Create a graph based on two elements
lets say we have "baa" and "abcd"

"b" and "a" does not match
means "b" comes before "a"
so we have "b" -> "a"

Similary form all edges and return topo sort
```
```
TC: O(v*e)
SC: O(v*e) ~> graph and o(v) ~> Visited arr
```

### Solution
```python
def findOrder(self, words, N, K):
    graph = {c: set() for w in words for c in w}
    
    for i in range(len(words)-1):
        w1, w2 = words[i], words[i+1]
        min_len = min(len(w1), len(w2))
        if len(w1) > len(w2) and w1[:min_len] == w2[:min_len]:
            return ""
        
        for j in range(min_len):
            if w1[j] != w2[j]:
                graph[w1[j]].add(w2[j])
                break
        
        visit = {}
        res = []
        
        def dfs(c):
            if c in visit:
                return visit[c]
                
            visit[c] = True
            
            for each in graph[c]:
                if dfs(each):
                    return True
            
            visit[c] = False
            res.append(c)
            
    for c in graph:
        if dfs(c):
            return ""
            
    return "".join(res[::-1])
```
