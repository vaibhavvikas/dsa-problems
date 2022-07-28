## 140. Word Break II

Given a string s and a dictionary of strings, construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.

### Algorithm
```bash
Step 1. Create a set of wordDict

Step 2. inititate the queue with queue = deque([(0, [])])
    the empty list signifies there are no words as of now.

Then the same logic as the BFS solution of word ladder,

Step 3. Pop the queue:
    on every match, also add the matched word 
    to the list along with the updated ind.
```
```bash
Example:

S = "catsanddog"
worddict = ["cat","cats","and","sand","dog"]

start -> deque([(0, [])])

deque([(3, ['cat']), (4, ['cats'])])
deque([(4, ['cats']), (7, ['cat', 'sand'])])
deque([(7, ['cat', 'sand']), (7, ['cats', 'and'])])
deque([(7, ['cats', 'and']), (10, ['cat', 'sand', 'dog'])])
deque([(10, ['cat', 'sand', 'dog']), (10, ['cats', 'and', 'dog'])])
deque([(10, ['cats', 'and', 'dog'])])
As soon as I reached the end i.e. start_ind = len(s), simple added to res set
```
```bash
TC: O(n^3)
SC: O(n)
```

### Solution
```python
def word_break_ii(s, wordDict):
    words = set(wordDict)
    queue = deque([(0, [])])
    res = set()
    
    while queue:
        start_ind, curr_words = queue.popleft()
        
        if start_ind == len(s):
            res.add(" ".join(curr_words))

        for end in range(start_ind + 1, len(s) + 1):
            word = s[start_ind: end] 
            if word in words:
                if not end in visited:
                    queue.append((end, curr_words + [word]))

    return res
```
