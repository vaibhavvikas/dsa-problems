## Trie with count of pref and words

Design a trie data structure, with the features

- Insert
- Count words equal to
- Count words start with
- Erase



### Algorithm
```
We main the Node with two
values end_count and pref_count

Each time we pass from a word,
we increment pref_count

At the end of word we increment
end_count

For erase: we decrement pref_count
At end we decrement end_count
```

```
TC: O(word_len)
```

### Solution
```python
class Node:
    def __init__(self):
        self.links = {}
        self.end_word = 0
        self.pref_count = 0
    
    def exists_key(self, char):
        return char in self.links
    
    def add(self, char, node):
        self.links[char] = node
    
    def get_key(self, char):
        return self.links[char]
    
    def add_pref(self):
        self.pref_count += 1
        
    def rem_pref(self):
        self.pref_count -= 1
        
    def set_end(self):
        self.end_word += 1
     
    def rem_end(self):
        self.end_word -= 1
        
    def get_end(self):
        return self.end_word
    
    def get_pref(self):
        return self.pref_count
    
class Trie:
    def __init__(self):
        self.root = Node()

    def insert(self, word):
        node = self.root
        for char in word:
            if not node.exists_key(char):
                node.add(char, Node())
            node.add_pref()
            node = node.get_key(char)
        node.add_pref()
        node.set_end()

    def countWordsEqualTo(self, word):
        node = self.root
        for char in word:
            if not node.exists_key(char):
                return 0
            node = node.get_key(char)
        return node.get_end()

    def countWordsStartingWith(self, word):
        node = self.root
        for char in word:
            if not node.exists_key(char):
                return 0
            node = node.get_key(char)
        return node.get_pref()

    def erase(self, word):
        node = self.root
        for char in word:
            node = node.get_key(char)
            node.rem_pref()
        node.rem_end()
```