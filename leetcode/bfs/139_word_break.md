## 139. Word Break

Given a string s and a dictionary of strings, return true if s can be broken into a space-separated sequence of one or more dictionary words.

```
Example:
word: "applepen", word_dict: ["apple", "pen", "pple"]
return: True
```

### Dynamic Programming

**Algorithm:**
```bash
Step 1. Create a DP array of size + 1

Step 1. Set last to True as empty can be formed
    start from last element to 0th element
    for each index check all the wwords:
    i.e. word[i+ len(word)] is in word_dict
    if its true => dp[i] = dp[i+len(w)]
    i.e. Its true if all the words after it,
    is also there

Step 3. If we find a True, we simply break
    as we need not to bother

Step 4. return dp[0] all the elements can
    be formed.
```
```bash
TC: O(n^3)
SC: O(n)
```

**Solution:**
```python
def word_break(s, word_dict):
    n = len(s)
    dp = [False]*(n+1)
    dp[-1] = True

    for i in range(n-1, -1, -1):
        for w in word_dict:
            if i + len(w) <= n:
                if s[i:i+len(w)] == w:
                    dp[i] = dp[i+len(w)]
                if dp[i]:
                    break

    return dp[0]
```

### Breadth First Search (BFS)

**Algorithm:**
```bash
Step 1. Create a set of word_dict
    Create a visited set()

Step 2. Initialize queue with 0

Step 3. while queue ->
    we check for range queue_ele + 1
    to len of word + 1:
    if word[start: end] is in word_dict
    we check if the end is already vis
    if not put it into queue

Step 4. In any case we reach the end
    of our word, we return True
```
```bash
TC: O(n^3)
SC: O(n)
```

**Solution:**
```python
def word_break(s, word_dict):
    n = len(s)
    words, visited = set(word_dict), set()
    queue = collections.deque([0])
    visited.add(0)

    while queue:
        ind = queue.pop()
        for end in range(ind + 1, n + 1):
            if s[ind:end] in words:
                if end not in visited:
                    queue.append(end)
                    visited.add(end)
                if end == n:
                    return True
    return False
```
