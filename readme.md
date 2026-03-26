### Question 3 Number of Islands

This is a graph problem. You can approach this problem using DFS or BFS. Both will yield the same time complexity O(M * n).

This is the DFS approach. The idea is that for each "1" that we encounter in the double for loop, that means that it is a new island that we have not seen before, we perform DFS on the entire island (any "1"'s that are connected to the starting point) and mark them as visited, so that when we finish DFS on that island, the connected 1's don't start a new DFS traversal since we have visited.
```
py
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
              dfs(row,col)
              islands += 1
  
  return islands
```
