# Random Point in Non-Overalapping Rectangles

[Problem Link](https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/description/) 

Given a list of non-overlapping rectangles, design a system to randomly pick a point within the space covered by these rectangles. 
Each point inside the rectangles should have an equal probability of being selected.



### Sample Input 
```
["Solution", "pick", "pick", "pick", "pick", "pick"]
[[[[-2, -2, 1, 1], [2, 2, 4, 6]]], [], [], [], [], []]
```
### Sample Output 
```
[null, [1, -2], [1, -1], [-1, -2], [-2, -2], [0, 0]]
```

### Solution
```java
class Solution {
private int[][] rects; // Store the rectangles
    private int[] areas;  // Store cumulative areas for weighted random selection
    private Random random;

    // Constructor: Initializes the object with the given rectangles
    public Solution(int[][] rects) {
        this.rects = rects;
        this.areas = new int[rects.length];
        this.random = new Random();

        // Calculate cumulative areas for weighted random selection
        int totalArea = 0;
        for (int i = 0; i < rects.length; i++) {
            int width = rects[i][2] - rects[i][0] + 1;  // Width of rectangle
            int height = rects[i][3] - rects[i][1] + 1; // Height of rectangle
            totalArea += width * height;
            areas[i] = totalArea; // Store cumulative area
        }
    }

    // Method: Picks a random point from the rectangles
    public int[] pick() {
        // Generate a random number in the range [0, totalArea)
        int target = random.nextInt(areas[areas.length - 1]);

        // Find the rectangle corresponding to the random number
        int rectIndex = binarySearch(target);

        // Select a random point within the chosen rectangle
        int[] rect = rects[rectIndex];
        int x = rect[0] + random.nextInt(rect[2] - rect[0] + 1); // Random x
        int y = rect[1] + random.nextInt(rect[3] - rect[1] + 1); // Random y

        return new int[]{x, y};
    }

    // Helper method: Binary search to find the rectangle based on target area
    private int binarySearch(int target) {
        int left = 0, right = areas.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (areas[mid] > target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

### Accepted
![Screenshot 2025-01-02 at 9 33 58 PM](https://github.com/user-attachments/assets/47c11a91-9076-4055-80e4-bb21ecab98eb)
