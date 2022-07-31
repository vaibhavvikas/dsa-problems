## Implement a Trie Data Structure

### Algorithm
```
We create a root with root being a blank
Trie node.

We create a dummy pointer to root for
each step

Insert: 
We run a loop from 0 to len(word)
if word[i] is not in node.links() ->
    insert
else simply use that word and go one
    step ahead
After the loop ends make the end flag
    True

Search:
Similarly, here if the word is not in
node.links ~> return False
In the end check if we have the flag
as True

Prefix:
Similar to search but not check end is
True
```

```bash
l = len of (word)
n = all the words

TC: Insert ~> O(l)
    Search ~> O(l)
    Prefix ~> O(l)

We generally dont bother about
space in Trie
SC: O(26 * l * n)
    At worst case all keys
    from "a" to "z" will be
    in dictionary.
```

### Solution
```python
class Node:
    def __init__(self):
        self.links = {}
        self.flag = False
    
    def contains_key(self, key):
        return key in self.links
    
    def put(self, char, node):
        self.links[char] = node
        
    def get(self, char):
        return self.links[char]
    
    def set_end(self):
        self.flag = True
    
    def is_end(self):
        return self.flag


class Trie :
    def __init__(self) :
        self.root = Node()
    
    def insert(self, string) :
        node = self.root
        for i in range(len(string)):
            if not node.contains_key(string[i]):
                node.put(string[i], Node())
            node = node.get(string[i])
        node.set_end()
        
    def search(self, word) :
        node = self.root
        for i in range(len(word)):
            if not node.contains_key(word[i]):
                return False
            node = node.get(word[i])
        return node.is_end()
        
    def startWith(self, prefix) :
        node = self.root
        for i in range(len(prefix)):
            if not node.contains_key(prefix[i]):
                return False
            node = node.get(prefix[i])
        return True
```
