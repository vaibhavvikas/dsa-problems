## Merge Overlapping Intervals

Problem Statement: Given an array of intervals, merge all the overlapping intervals and return an array of non-overlapping intervals.

```bash
Examples:
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
```
### Algorithm
```
TC: O(nlogn) + O(n)
SC: O(n)
```


### Solution
```python
def merge_intervals(intervals):
    intervals.sort()
    res = [intervals[0]]

    for i in range(1, len(intervals)):
        if interval[i][0] <= res[-1][1]:
            res[-1][1] = max(interval[i][1], res[-1][1])
        else:
            res.append(intervals[i])

    return res
```
