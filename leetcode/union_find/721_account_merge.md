## 721. Account Merge

```bash
Example
Input: accounts = [["John","johnsmith@mail.com","john_newyork@mail.com"],
        ["John","johnsmith@mail.com","john00@mail.com"],
        ["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Output: [["John","john00@mail.com","john_newyork@mail.com","johnsmith@mail.com"],
        ["Mary","mary@mail.com"],
        ["John","johnnybravo@mail.com"]]
```

### We Union Find

1. Traverse over each account, and for each account, traverse over all of its emails. If we see an email for the first time, then set the group of the email as the index of the current account in emailGroup.
2. Otherwise, if the email has already been seen in another account, then we will union the current group (i) and the group the current email belongs to (emailGroup[email]).
3. After traversing over every account and merging the accounts that share a common email, we will now traverse over every email once more. Each email will be added to a map (components) where the key is the email's representative, and the value is a list of emails with that representative.
4. Traverse over components, here the keys are the group indices and the value is the list of emails belonging to this group (person). Since the emails must be "in sorted order" we will sort the list of emails for each group. Lastly, we can get the account name using the accountList[group][0]. In accordance with the instructions, we will insert this name at the beginning of the email list.
5. Store the list created in step 4 in our final result (mergedAccount).

```
TC: O(NKlogNK)
SC: O(NK)
```

```python
class UnionFind:
    def __init__(self, n):
        self.parent = {i:i for i in range(n)}
        self.rank = [0 for _ in range(n)]
    
    def union(self, u, v):
            par_u, par_v = self.find(u), self.find(v)
            
            if par_u == par_v:
                return
            
            if self.rank[par_u] < self.rank[par_v]:
                self.parent[par_u] = par_v
            elif self.rank[par_u] > self.rank[par_v]:
                self.parent[par_v] = par_u
            else:
                self.parent[par_u] = par_v
                self.rank[par_v] += 1
                
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
        
def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
    n = len(accounts)
    uf = UnionFind(n)
    
    email_group = {}
    
    for i in range(n):
        account_size = len(accounts[i])
        for j in range(1, account_size):
            email = accounts[i][j]
            
            if email not in email_group:
                email_group[email] = i
            else:
                uf.union(i, email_group[email])    
    
    group_emails_dict = defaultdict(list)
    for email, group in email_group.items():
        group_parent = uf.find(group)
        group_emails_dict[group_parent].append(email)
        
    accounts_merged = []
    for group, emails in group_emails_dict.items():
        name = accounts[group][0]
        accounts_merged.append([name] + sorted(emails))
        
    return accounts_merged
```
