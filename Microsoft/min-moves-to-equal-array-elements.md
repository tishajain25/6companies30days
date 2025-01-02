# Mininum Moves to Equal Array Elements

[Problem Link](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/description/) 

Given an integer array nums, find the minimum number of moves required to make all elements in the array equal.
In one move, you can increment or decrement an element by 1.

### Sample Input
```
nums = [1, 2, 3]
```
### Sample Output
```
2
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
![Screenshot 2025-01-02 at 1 20 10 PM](https://github.com/user-attachments/assets/e3a4742e-3007-46c2-9c50-2bdf08776d9c)
