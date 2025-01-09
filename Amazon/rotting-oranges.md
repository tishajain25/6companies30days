# Rotting Oranges

[Problem Link](https://leetcode.com/problems/rotting-oranges/description/) 

You are given an m x n grid representing oranges:

0: Empty cell.
1: Fresh orange.
2: Rotten orange.

Each minute, fresh oranges adjacent to rotten ones (up, down, left, right) become rotten. Find the minimum time to rot all fresh oranges. If it's impossible, return -1.

### Sample Input 1
```
grid = [[2,1,1],[1,1,0],[0,1,1]]
```
### Sample Output 1
```
4
```

### Sample Input 2
```
grid = [[2,1,1],[0,1,1],[1,0,1]]
```
### Sample Output 2
```
-1
```

### Solution
```java
class Solution {
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        // Queue to store rotten oranges
        Queue<int[]> queue = new LinkedList<>();
        int freshOranges = 0;

        // Initialize the queue with all rotten oranges and count fresh oranges
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 2) {
                    queue.add(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    freshOranges++;
                }
            }
        }

        // Directions for moving up, down, left, right
        int[][] directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        int minutes = 0;

        // BFS to rot adjacent fresh oranges
        while (!queue.isEmpty() && freshOranges > 0) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int[] current = queue.poll();
                int x = current[0];
                int y = current[1];

                for (int[] direction : directions) {
                    int newX = x + direction[0];
                    int newY = y + direction[1];

                    // Check if the new cell is within bounds and has a fresh orange
                    if (newX >= 0 && newX < rows && newY >= 0 && newY < cols && grid[newX][newY] == 1) {
                        grid[newX][newY] = 2; // Mark as rotten
                        queue.add(new int[]{newX, newY});
                        freshOranges--; // Reduce the count of fresh oranges
                    }
                }
            }
            minutes++;
        }

        // If there are still fresh oranges left, return -1
        return freshOranges == 0 ? minutes : -1;
    }
}
```

### Accepted
![Screenshot 2025-01-09 at 2 00 35 PM](https://github.com/user-attachments/assets/ca524aac-4c7c-4c55-ad63-177d2e1dc1e3)
