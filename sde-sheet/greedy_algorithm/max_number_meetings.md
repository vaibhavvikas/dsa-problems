## Max number of meetings

There is one meeting room in a firm. There are N meetings in the form of (start[i], end[i]) where start[i] is start time of meeting i and end[i] is finish time of meeting i.
What is the maximum number of meetings that can be accommodated in the meeting room when only one meeting can be held in the meeting room at a particular time?

Note: Start time of one chosen meeting can't be equal to the end time of the other chosen meeting.

```bash
Example:

Input:
N = 6
start[] = {1,3,0,5,8,5}
end[] =  {2,4,6,7,9,9}

Output: 4
```

### Approach
```bash
First we create a meeting_arr

Now we sort it based on the
end time and add the first
meeting in a new list

Now before adding any new
item to it we check if the
end time is less than the new
start time.
```
```bash
TC: O(n) + O(nlogn) + O(n)
SC: O(n) + O(n)
```

### Solution
```python
def maximumMeetings(n, start, end):
    meeting = []
    for i in range(n):
        meeting.append((start[i], end[i]))
        
    meeting.sort(key = lambda x: x[1])
    selected_meet = [meeting[0]]
    
    for i in range(1, n):
        if selected_meet[-1][1] < meeting[i][0]:
            selected_meet.append(meeting[i])
            
    return len(selected_meet)
```
