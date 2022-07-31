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

Now for each char in graph, we use dfs.
to check cycle.
```
```
TC: O(n*k)
SC: O(n+k) ~> graph and o(k) ~> Visited arr
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


### BFS Approach

#### Algorithm
```
Initialize the graph using 
a set of characters using words

Like previous for each word if
char is different add in graph

calculate indegree
initialize cnt = 0

put all edges with indegree 0 
in queue. And find topo sort
```
```bash
TC: O(n*k)
SC: O(n+k) ~> graph 
    + O(k) ~> indegree
    + O(k) ~> queue
```
#### Solution

```python
class Graph:
    def __init__(self, words):
        self.adj = {c: set() for w in words for c in w}
        self.indegree = defaultdict(int)
        
    def add_edge(self, source, dest):
        self.adj[source].add(dest)
        
    def calculate_indegree(self):
        for source in self.adj:
            self.indegree[source] += 0
            for dest in self.adj[source]:
                self.indegree[dest] += 1

    def get_indegree(self, char):
        return self.indegree[char]

    def dec_indegree(self, char):
        self.indegree[char] -= 1
    
    def get_neighbours(self, char):
        return self.adj[char]
    

class Solution:
    def findOrder(self, words, N, K):
        graph = Graph(words)
        
        for i in range(len(words)-1):
            w1, w2 = words[i], words[i+1]
            min_len = min(len(w1), len(w2))
            if len(w1) > len(w2) and w1[:min_len] == w2[:min_len]:
                return ""
            
            for j in range(min_len):
                if w1[j] != w2[j]:
                    graph.add_edge(w1[j], w2[j])
                    break
            
        graph.calculate_indegree()
        
        visited = set()
        res = []
        cnt = 0
            
        queue = deque([])
        for char in graph.indegree:
            if graph.get_indegree(char) == 0:
                queue.append(char)
                
        while queue:
            curr = queue.popleft()
            res.append(curr)

            for neighbour in graph.get_neighbours(curr):
                if neighbour not in visited:
                    graph.dec_indegree(neighbour)
                    if graph.get_indegree(neighbour) == 0:
                        queue.append(neighbour)
                        visited.add(neighbour)
            cnt += 1
        
        if cnt != K:
            return ""

        return "".join(res)
```
