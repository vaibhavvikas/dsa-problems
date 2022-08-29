## 128. Word Ladder 2

### Algorithms

```
Using Same as Word Ladder I
Giving TLE on Leetcode for 
last testcase
```
```
TC: O(n*n*m)
SC: O(n*m + n)
```

### Solution
```python
def findLadders(beginWord: str, endWord: str, wordList):
    if endWord not in wordList or beginWord not in wordList:
        return []

    combo = defaultdict(list)
    for word in wordList:
        for j in range(len(word)):
            pattern = word[:j] + "_" + word[j+1:]
            combo[pattern].append(word)

    visited = set()
    queue = deque([(beginWord, [beginWord])])
    
    res = []
    
    while queue:
        local_visited = set()
        for _ in range(len(queue)):
            word, list_so_far = queue.popleft()

            for j in range(len(word)):
                pattern = word[:j] + "_" + word[j+1:]
                
                for neighbour in combo[pattern]:
                    if neighbour == endWord:
                        res.append(list_so_far + [neighbour])
                        continue

                    if neighbour not in visited:
                        queue.append((neighbour, list_so_far + [neighbour]))
                        local_visited.add(neighbour)

        visited = visited.union(local_visited)
    return res
```