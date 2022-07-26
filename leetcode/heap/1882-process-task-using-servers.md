## 1882. Process tasks using servers

**Given:** 
server arr with each ind corresponding to its weight
task_queue: each ind is time taken to run that task

**Objective:**
create a res arr with each ind corresponding to the server
ind it is assigned to.


```python
Constraints:

servers.length == n
tasks.length == m
1 <= n, m <= 2 * 105
1 <= servers[i], tasks[j] <= 2 * 105
```

### Algorithm

```python
1. Create a min_heap, push the (load, ind)
2. Create a timer = 0, and make it max(timer, curr_task_ind)
3. We have three cases:
   Case 1: Extend time to a great time since we cant do anything.
   Case 2: Check if occupied server is complete. then push that server.
4. we need to choose a server and push the element there
```
```python
TC: O(mn) ~> worst case when there is no free server. 
SC: O(m) ~> heaps
```

### Solution

```python
def assignTasks(servers: List[int], tasks: List[int]) -> List[int]:
    res = []
    timer = 0
    
    free_server, occupied_server = [], []

    for ind, load in enumerate(servers):
        heapq.heappush(free_server, (load, ind))

    for j, task_time in enumerate(tasks):
        timer = max(timer, j)
        
        # Extend time to a great time since we cant do anything:
        if not free_server and occupied_server[0][0] >= timer:
            timer = occupied_server[0][0]
        
        # Check if occupied first element is complete.
        while occupied_server and occupied_server[0][0] == timer:
            _, ind = heapq.heappop(occupied_server)
            heapq.heappush(free_server, (servers[ind], ind))
        
        # Case: we need to choose a server and push the element there
        server_load, server_ind = heapq.heappop(free_server)
        time_taken = timer + task_time
        heapq.heappush(occupied_server, (time_taken, server_ind))
        res.append(server_ind)

    return res
```