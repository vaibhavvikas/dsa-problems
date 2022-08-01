## 207. Course Schedule

There are n courses you have to take, labeled from 0 to n - 1. You are given prerequisites array where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

Return True if you can complete all courses.

### Algorithm
```
BFS Topological Sort
```
```
TC: O(V+E)
SC: O(V)
```
### Solution

```python
def canFinish(self, numCourses: int, prerequisites):
    adj = defaultdict(list)
    indegree = defaultdict(int)
    
    for source, dest in prerequisites:
        adj[source].append(dest)
        indegree[dest] += 1

    queue = deque([])
    
    for i in range(numCourses):
        if indegree[i] == 0:
            queue.append(i)
    
    if not queue:
        return False
    
    cnt = 0
    
    while queue:
        course = queue.popleft()
        for neighbour in adj[course]:
            indegree[neighbour] -= 1
            if indegree[neighbour] == 0:
                queue.append(neighbour)
        cnt += 1
    
    return cnt == numCourses
```