## 2050. Parallel Courses III

There are n courses labeled from 1 to n
time corresponds to each course
relations representing dependency of courses

Find min time to complete all courses

### Algorithm
```bash
Kahn Algo + MinHeap
Step 1: Create adj and indegree
Step 2: Create a min heap with time taken as its
        priority
Step 3. Pop the heap and change the curr_time and
        update indegree based on that
Step 4. If indegree becomes zero push it to heap
        updating its time by adding curr_time
        to it
```
```bash
TC ~> O(n^2)
SC ~> O(mn) + O(n) + O(n)
```

### Solution
```python
def minimumTime(self, n, relations, time:):
    adj, indegree  = defaultdict(list), defaultdict(int)
    
    for source, dest in relations:
        adj[source].append(dest)
        indegree[dest] += 1
        
    heap = []
    
    for course in range(1, n+1):
        if course not in indegree:
            heapq.heappush(heap, (time[course-1], course))
    
    min_time = 0
    
    while heap:
        time_taken, course = heapq.heappop(heap)
        min_time = time_taken
        
        for next_course in adj[course]:
            indegree[next_course] -= 1
            if indegree[next_course] == 0:
                heapq.heappush(heap, (time[next_course-1] \
                    + min_time, next_course))
    
    return min_time
```
