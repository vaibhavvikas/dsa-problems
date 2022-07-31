## Dijkstra's Algorithm

Find shortest path between source and destination using Dijkstra's algorithm.

### Algorithm

```
Expanding shortest path algprithm 
using priority queue

We keep a distance array.
and before pushing the eleemnt
in the priority queue we check 
if its distance is less than 
what was before.
```
```
TC: O(ElogV)
SC: O(V) + O(V)
```

### Solution
```python
def find_min_dis(graph, source, dest):
    heap = [(0, source)]
    path_distance = [math.inf]*(len(graph)+1)
    path_distance[0] = 0

    while heap:
        distance, node = heapq.heappop(heap)

        for nei, dis in graph[node]:
            if distance + dis < path_distance[nei]:
                path_distance[nei] = distance + dis
                heapq.heappush(heap, (path_distance[nei], nei))

    return path_distance[dest]
```