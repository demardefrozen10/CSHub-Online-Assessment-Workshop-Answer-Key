### Question 3 Number of Islands

This is a graph problem. You can approach this problem using DFS or BFS. Both will yield the same time complexity O(M * n). The idea is that for each "1" that we encounter in the double for loop, that means that it is a new island that we have not seen before, we perform DFS/BFS on the entire island (any "1"'s that are connected to the starting point) and mark them as visited, so that when we finish DFS/BFS on that island, the connected 1's don't start a new DFS/BFS traversal since we have visited and it is not a seperate island (since it is connected). The reason why both works is because eventually both will traverse the island completely, just a matter of which one traverses which parts first (DFS is DEPTH first, BFS is BREADTHE first).


This is the DFS approach. 
```python
def numIslands(islands):
  rows, cols = len(islands), len(islands[0])
  
  islands = 0
  visited = set()
  
  def dfs(i,j):
      neighbors = [(i+1, j), (i-1,j), (i,j+1), (i,j-1)]
      for row, col in neighbors:
          if row >=0 and row < rows and col >=0 and col < cols and (row,col) not in visited and islands[row][col] == "1":
              visited.add((row,col))
              dfs(row,col)
  
  for row in range(rows):
      for col in range(cols):
          if islands[row][col] == "1" and (row,col) not in visited:
              visited.add((row,col))
              dfs(row,col)
              islands += 1
  
  return islands
```
```java
    public static int numIslands(List<List<String>> islands) {
        int m = grid.size();
        int n = grid.get(0).size();
        int c = 0;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(grid[i][j] == '1'){
                    dfs(grid, i, j);
                    c++;
                }
            }
        }
        return c;
    }
    

    public void dfs(List<List<String>> islands, int i, int j) {
        int m = islands.size();
        int n = islands.get(0).size();
        if(i < 0 || j < 0 || i >= m || j >= n || islands.get(i).get(j) == '0'){
            return;
        }
        islands.get(i).set(j, '0'); // mark it as visited
        dfs(islands, i+1, j);
        dfs(islands, i-1, j);
        dfs(islands, i, j+1);
        dfs(islands, i, j-1);
    }
```


This is the BFS approach. 
```python
def numIslands(islands):
  rows, cols = len(islands), len(islands[0])
  
  islands = 0
  visited = set()
  
  queue = deque()
  for x in range(rows):
      for y in range(cols):
          if islands[x][y] == "1" and (x,y) not in visited:
              queue.appendleft((x,y)) # Start of BFS
              while queue: # While loop is the entire BFS algorithm
                  i,j = queue.pop()
                  neighbors = [(i+1, j), (i-1,j), (i,j+1), (i,j-1)]
                  for row, col in neighbors:
                      if row >=0 and row < rows and col >=0 and col < cols and (row,col) not in visited and islands[row][col] == "1":
                          queue.appendleft((row,col))
                          visited.add((row,col))
              islands += 1
  
  return islands
```
