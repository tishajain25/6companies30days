# Minimum Number of Days to Disconnect Island

[Problem Link](https://leetcode.com/problems/minimum-number-of-days-to-disconnect-island/description/) 

You are given a 2D grid where:

. 1 represents land.
. 0 represents water.

An island is a group of connected 1s. The grid is connected if there is exactly one island. Your task is to determine the minimum 
number of days required to disconnect the grid by turning land cells (1) into water (0).

A grid is disconnected if:

1. There are multiple islands.
2. There are no islands at all.

### Sample Input 1
```
grid = [[0,1,1,0],
        [0,1,1,0],
        [0,0,0,0]]
```
### Sample Output 1
```
2
```

### Sample Input 2
```
grid = [[1,1]]
```
### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    public int minDays(int[][] grid) {
        int m = grid.length, n = grid[0].length;

        // Check if the grid is already disconnected
        if (!isConnected(grid)) return 0;

        // Check if removing one cell disconnects the grid
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    grid[i][j] = 0; // Temporarily remove the land
                    if (!isConnected(grid)) return 1;
                    grid[i][j] = 1; // Restore the land
                }
            }
        }

        // If one removal doesn't work, at most 2 removals are required
        return 2;
    }

    // Check if the grid is connected (contains exactly one island)
    private boolean isConnected(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        boolean[][] visited = new boolean[m][n];
        int islandCount = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1 && !visited[i][j]) {
                    if (islandCount > 0) return false; // More than one island
                    dfs(grid, i, j, visited);
                    islandCount++;
                }
            }
        }
        return islandCount == 1; // Return true if exactly one island
    }
    // DFS to traverse the island
    private void dfs(int[][] grid, int i, int j, boolean[][] visited) {
        int m = grid.length, n = grid[0].length;
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 0 || visited[i][j]) {
            return;
        }
        visited[i][j] = true;
        dfs(grid, i + 1, j, visited);
        dfs(grid, i - 1, j, visited);
        dfs(grid, i, j + 1, visited);
        dfs(grid, i, j - 1, visited);
    }
}
```

### Accepted
![Screenshot 2025-01-17 at 1 32 42 PM](https://github.com/user-attachments/assets/e278cd16-f91d-43e0-989f-38efe2fff602)
