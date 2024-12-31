# Circle and Rectangle Overlapping

[Problem Link](https://leetcode.com/problems/circle-and-rectangle-overlapping/description/) 

Given a circle represented by its radius and center coordinates (radius, xCenter, yCenter), and a rectangle represented by 
its bottom-left and top-right corner coordinates (x1, y1, x2, y2), determine if the circle and rectangle overlap. Return true 
if they overlap, otherwise return false.



### Sample Input 1
```
radius = 1, xCenter = 0, yCenter = 0, x1 = 1, y1 = -1, x2 = 3, y2 = 1
```
### Sample Output 1
```
true 
```

### Sample Input 2
```
radius = 1, xCenter = 1, yCenter = 1, x1 = 1, y1 = -3, x2 = 2, y2 = -1
```
### Sample Output 2
```
false 
```

### Solution
```java
class Solution {
    public boolean checkOverlap(int radius, int xCenter, int yCenter, int x1, int y1, int x2, int y2) {
        // Find the closest point on the rectangle to the center of the circle
        int closestX = Math.max(x1, Math.min(xCenter, x2)); // Closest X coordinate on rectangle
        int closestY = Math.max(y1, Math.min(yCenter, y2)); // Closest Y coordinate on rectangle
        
        // Calculate the distance from the center of the circle to the closest point on the rectangle
        int dx = xCenter - closestX;
        int dy = yCenter - closestY;
        
        // If the distance is less than or equal to the radius, the circle and rectangle overlap
        return dx * dx + dy * dy <= radius * radius;
    }
}
```

### Accepted
![Screenshot 2024-12-31 at 10 36 42 PM](https://github.com/user-attachments/assets/ff3d554e-b739-40df-abe3-fa0fffe0bf13)
