## Longest Common Subsquence

### Problem Statement

Given two strings, 'S' and 'T' with lengths 'M' and 'N', find the length of the 'Longest Common Subsequence'.

For a string 'str'(per se) of length K, the subsequences are the strings containing characters in the same relative order as they are present in 'str,' but not necessarily contiguous. Subsequences contain all the strings of length varying from 0 to K.

Example:
```bash
Subsequences of string "abc" are:
""(empty string), a, b, c, ab, bc, ac, abc.
```

Input Format:
```bash
The first line of input contains the string 'S' of length 'M'.
The second line of the input contains the string 'T' of length 'N'.
```

Output Format :
```
Return the length of the Longest Common Subsequence.
```

Constraints :
```python
0 <= M <= 10 ^ 3
0 <= N <= 10 ^ 3
Time Limit: 1 sec
```

Sample Input 1 :
```
adebc
dcadb
```

Sample Output 1 :
```
3
```

Explanation Of The Sample Output 1:
```bash
Both the strings contain a common subsequence 'adb',
which is the longest common subsequence with length 3.
```

### Algorithm Recursion:

```python
Recursion: Top Down
Step 1: Convert problem to indexes
    Here we have two last indexes:
    of both string s and t

Step 2: Explore Possibilities:
    and take the best for each

On each step we have 2 cases:
Case 1: Matches
    if it happens we decrement both
    and return 1 + the result

Case 2: Non match:
    decrement either and return max

Base Case:
    if ind < 0: return 0
```

### Solution

```python
# Recursion: Top Down
# TC: exponential: 2^n
# O(1) but its taking auxiliary stack space O(2^n)

def lcs(s, t) :
    s_length, t_length = len(s), len(t)
    
    def find_lcs_length(s_ind, t_ind):
        if s_ind < 0 or t_ind < 0:
            return 0
        
        # Case 1: Match
        if s[s_ind] == t[t_ind]:
            return 1 + find_lcs_length(s_ind-1, t_ind-1)
        
        # Case 2: No Match
        return max(find_lcs_length(s_ind-1, t_ind),\
                   find_lcs_length(s_ind, t_ind-1))
    
    return find_lcs_length(s_length-1, t_length-1)
```

```python
# Memoization
# TC: O(mn)
# Space: O(mn) + Recursion Aux Stack Space O(m+n)

def lcs(s, t):
    s_length, t_length = len(s), len(t)

    dp = [[-1]*t_length for _ in range(s_length)]
    
    def find_lcs_length(s_ind, t_ind):
        if s_ind < 0 or t_ind < 0:
            return 0
        
        if dp[s_ind][t_ind] != -1:
            return dp[s_ind][t_ind]
        
        # Case 1: matches
        if s[s_ind] == t[t_ind]:
            dp[s_ind][t_ind] = 1 + find_lcs_length(s_ind-1, t_ind-1)
            return dp[s_ind][t_ind]
        
        # Case 2: Not mathces
        dp[s_ind][t_ind] = max(find_lcs_length(s_ind-1, t_ind),\
                               find_lcs_length(s_ind, t_ind-1))
        return dp[s_ind][t_ind]
    
    return find_lcs_length(s_length-1, t_length-1)
```

### Algorithm Tabulation:
```python
Tabulation: Bottom Up
Step 1: Copy the base cases:
    for that we incremented the index of dp
    i.e. we took the size of len string + 1
    i.e Shifting right

Step 2: Changing params in opp manner:
    Start from 1 to len(string) + 1

Step 3: Copy the recurrence
```

### Solution:

```python
# Tabulation
# TC: O(mn)
# SC: O(mn)

def lcs(s, t):
    s_length, t_length = len(s), len(t)
    
    dp = [[0]*(t_length+1) for _ in range(s_length+1)]
    
    for i in range(1, s_length+1):
        for j in range(1, t_length+1):
            if s[i-1] == t[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[-1][-1]
```
