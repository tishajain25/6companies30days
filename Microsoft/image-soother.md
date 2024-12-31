# Image Soother

[Problem Link](https://leetcode.com/problems/image-smoother/description/) 

An image smoother is a filter of size 3 x 3 that can be applied to each cell of an image by rounding down the average of the cell and the eight surrounding cells. 
If one or more surrounding cells of a cell are not present, they are not included in the average.


### Sample Input
```
3 3  
1 1 1  
1 0 1  
1 1 1  
```
### Sample Output
```
3 3  
0 0 0  
0 0 0  
0 0 0  
```

### Solution
```java
class Solution {
    public int[][] imageSmoother(int[][] img) {
        int m = img.length;
        int n = img[0].length;
        int[][] result = new int[m][n];

        // Directions for 8 neighbors and the cell itself
        int[] dx = {-1, -1, -1, 0, 0, 0, 1, 1, 1};
        int[] dy = {-1, 0, 1, -1, 0, 1, -1, 0, 1};

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int sum = 0, count = 0;

                // Check all 9 cells (including itself)
                for (int k = 0; k < 9; k++) {
                    int x = i + dx[k];
                    int y = j + dy[k];

                    // Check if the neighboring cell is within bounds
                    if (x >= 0 && x < m && y >= 0 && y < n) {
                        sum += img[x][y];
                        count++;
                    }
                }

                // Calculate the average and floor it
                result[i][j] = sum / count;
            }
        }

        return result;
        
    }
}
```

### Accepted
![image](https://github.com/user-attachments/assets/9b1948a5-7d2e-4553-835c-2e0c087e85e1)
