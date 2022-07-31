## Shortest Path Unit Weights

Given a source and destination node.
Find the minimum distance if all the edges are of unit length.

### Algorithm BFS

```bash
Each time we visit the vertex,
we put in queue only if its distance
is less.
```
```bash
TC: O(v+e)
SC: O(v+e) + O(v)
```

### Solution

```python
def find_min_dis(graph, source, dest):
    queue = deque([0])
    distance = [math.inf]*len(graph)
    distance[source] = 0

    while queue:
        node = queue.popleft()

        for neighbour in graph[node]:
            if distance[neighbour] > distance[node] + 1:
                distance[neighbour] = distance[node] + 1
                queue.append(neighbour)

    return distance[dest] if distance[dest] != math.inf else -1
```