## 127. Word Ladder

A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that at each step only once change is there.

### Algorithm
```bash
Step 1. Take an example a word abc -> def
from     "abc"
      /    |    \
  "_bc", "a_c", "ab_"

We make a graph which shows
these patterns can be used to form the main word

Step 2. Take a visited array and a queue with
    start element at the beginWord

Step 3. If its equal to dest word return 0
    else: 
    Make all patters from that word,
    and append the word which can be
    formed by those patterss.

Step 4. On each level increment the steep by 1
```
```
TC: O(n*m) ~> number of words * len of words
SC: O(n*m) ~> graph + O(n) ~> visited + O(n) ~> queue
```

### Solution
```python
def ladderLength(beginWord, endWord, wordList):
    if endWord not in wordList:
        return 0
    
    graph = defaultdict(list)
    for word in wordList:
        for j in range(len(word)):
            pattern = word[:j] + "_" + word[j+1:]
            graph[pattern].append(word)
            
    visited = set(beginWord)
    queue = deque([beginWord])
    
    res = 1
    
    while queue:
        for _ in range(len(queue)):
            word = queue.popleft()
            if word == endWord:
                return res
            
            for j in range(len(word)):
                pattern = word[:j] + "_" + word[j+1:]
                for neighbour in graph[pattern]:
                    if neighbour not in visited:
                        queue.append(neighbour)
                        visited.add(neighbour)
        res += 1
        
    return 0   
```