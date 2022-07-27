## 2115. Find All Possible Recipes from Given Supplies

**Given:**
recipes and the ingredients for making it
supplies

**Objective:**
Return all recipes you can make

### Algorithm

```python
1. Make a graph where we have each indegree representing,
   supplies required to make it.

   recipes = ["bread", "sandwich"]
   ingredients = [["yeast","flour"], ["meat", "bread"]]
   supplies = ["yeast","flour","meat"]

   we can now draw the graph first.
   (Consider the graph directed from upper nodes to downwards)

				   yeast   flour
					  \    /
			meat      bread
			  \        /
			   sandwich

2. Mark indegree based on number of inwards nodes.
   bread => 2, sandwich => 2
3. Put all the elements from supplies in queue.
4. Start from queue and with each connection with that node,
   make indegree -= 1
5. If indegree becomes 0 means it can be made. So we put it in
   res set and also append it in queue that implies, we can use it
   as new supply.
```
```python
TC: O(n*m) ~> traversing queue
SC: O(n+m) ~> queue, O(n) ~> indegree and O(n*m) ~> adj matrix
```

### Solution:

```python
def findAllRecipes(recipes, ingredients, supplies):
    adj = defaultdict(list)
    indegree = defaultdict(int)
    
    for i in range(len(recipes)):
        for item in ingredients[i]:
            adj[item].append(recipes[i])
            indegree[recipes[i]] += 1

    possible_recipes = set()
    queue = deque(supplies)

    while queue:
        recipe = queue.popleft()
        for food_item in adj[recipe]:
            if indegree[food_item] >= 1:
                indegree[food_item] -= 1
            if indegree[food_item] == 0:
                queue.append(food_item)
                possible_recipes.add(food_item)
    
    return possible_recipes
```