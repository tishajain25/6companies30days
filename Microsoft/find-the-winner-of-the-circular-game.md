# Find the Winner of the Circular Game

[Problem Link](https://leetcode.com/problems/find-the-winner-of-the-circular-game/) 

Given n friends sitting in a circle, eliminate every kth friend in clockwise order until one remains. Return the position of the winner.

### Sample Input
```
n = 5, k = 2
```
### Sample Output
```
3 
```

### Solution
```java
class Solution {
    public int findTheWinner(int n, int k) {
        // Start with the base case: only one person left
        int winner = 0;
        
        // Iteratively calculate the winner for increasing number of friends
        for (int i = 2; i <= n; i++) {
            // Update the winner's position using the Josephus formula
            winner = (winner + k) % i;
        }
        
        // Convert the 0-based index to 1-based index
        return winner + 1;
    }
}
```

### Accepted
![Screenshot 2025-01-01 at 11 55 39 PM](https://github.com/user-attachments/assets/047a7803-75b7-475b-a861-0dd8be3c5f87)
