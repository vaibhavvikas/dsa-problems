## 472. Concatenated Words

Given an array of unique words, return all the concatenated words in the given list of words.

A concatenated word is comprised entirely of at least two shorter words in the given array.

### Algorithm

**[Word Break Approach](./139_word_break.md)**
```bash
We create a set of words for O(1) search
Now for each word in the list:
we remove it from set and test it by 
using the following word break intuition.

Step 1. Create a visited set()

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
```
TC: O(n^4): n^3 for each test and
    since its called by loop
SC: O(n) 
```

### Solution
```python
def findAllConcatenatedWordsInADict(words):
    words = set(words)
    res = []
        
    for word in words:
        words.remove(word)
        if check_word(word, words):
            res.append(word)
        words.add(word)

    return res

def check_word(word, words):
    queue = deque([0])
    visited = set([0])
    while queue:
        ind = queue.popleft()
        
        for end in range(ind + 1, len(word) + 1):
            if word[ind:end] in words:
                if end not in visited:
                    queue.append(end)
                    visited.add(end)
                if end == len(word):
                    return True
    return False
```
