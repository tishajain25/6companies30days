# Map of Highest Peak

[Problem Link](https://leetcode.com/problems/map-of-highest-peak/description/) 

You are given a matrix isWater of size m x n, where each cell is either water (1) or land (0). The goal is to assign a height to each cell such that:

1. Water cells have a height of 0.
2. Adjacent cells (north, south, east, west) have a height difference of at most 1.
3. The maximum height in the matrix is as large as possible.

Return the matrix of heights where each land cell has the maximum possible height under the given constraints.

### Sample Input 1
```
isWater = [[0, 1], [0, 0]]
```

### Sample Output 1
```
[[1, 0], [2, 1]]
```

### Sample Input 2
```
isWater = [[0, 0, 1], [1, 0, 0], [0, 0, 0]]
```

### Sample Output 2
```
[[1, 1, 0], [0, 1, 1], [1, 2, 2]]
```

### Solution
```java
class Solution {
    public int[][] highestPeak(int[][] isWater) {
      int m = isWater.length;
        int n = isWater[0].length;
        
        // Initialize the result matrix with -1, meaning unassigned
        int[][] height = new int[m][n];
        for (int[] row : height) {
            Arrays.fill(row, -1);
        }
        
        // Queue for BFS
        Queue<int[]> queue = new LinkedList<>();
        
        // Add all water cells to the queue and set their height to 0
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (isWater[i][j] == 1) {
                    height[i][j] = 0;
                    queue.offer(new int[]{i, j});
                }
            }
        }
        
        // Directions for North, South, East, West
        int[] dirs = {-1, 0, 1, 0, -1};
        
        // BFS to fill the height matrix
        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            int x = cell[0], y = cell[1];
            
            // Explore all 4 adjacent cells
            for (int i = 0; i < 4; i++) {
                int nx = x + dirs[i];
                int ny = y + dirs[i + 1];
                
                // Check if the new position is within bounds and hasn't been assigned a height
                if (nx >= 0 && nx < m && ny >= 0 && ny < n && height[nx][ny] == -1) {
                    // Assign the height as 1 greater than the current cell's height
                    height[nx][ny] = height[x][y] + 1;
                    queue.offer(new int[]{nx, ny});
                }
            }
        }
        
        return height;
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 20 37 PM](https://github.com/user-attachments/assets/2004cb76-1588-4bd1-9d91-7bf8cb90aae3)
