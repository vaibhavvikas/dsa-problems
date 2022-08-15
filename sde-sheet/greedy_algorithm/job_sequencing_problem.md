## Job Sequencing Problem

Given a set of N jobs where each jobi has a deadline and profit associated with it.
Each job takes 1 unit of time to complete and only one job can be scheduled at a time. We earn the profit associated with job if and only if the job is completed by its deadline.
Find the number of jobs done and the maximum profit.
Note: Jobs will be given in the form (Jobid, Deadline, Profit) associated with that Job.

```bash
Example:

Input:
Jobs = {(1,4,20),(2,1,10),(3,1,40),(4,1,30)}

Output:
2 60
```

### Approach
```bash
We sort the jobs based on decreasing
profits.
than we assign the first job at the last
based on its deadline.

After that we keep on decrementing
deadline and if its not present we 
assign the job there
```
```bash
TC: O(nlogn) + O(m*n)
SC: O(n)
```

### Solution
```python
def JobScheduling(Jobs, n):
    job_id = {}
    
    Jobs.sort(key = lambda x: x.profit, reverse=True)
    res = 0
    
    for job in Jobs:
        deadline = job.deadline
        while deadline in job_id:
            deadline -= 1
        
        if deadline >= 1:
            job_id[deadline] = job.profit
            res += job.profit
    
    return [len(job_id), res]
```
