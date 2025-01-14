# Battleships in a Board

[Problem Link](https://leetcode.com/problems/battleships-in-a-board/description/) 

Given an m×n grid board, where each cell is either 'X' (battleship) or '.' (empty), count the number of distinct battleships. 
Battleships can only be horizontal or vertical and cannot touch each other.

### Sample Input 1
```
board = [["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]
```
### Sample Output 1
```
2
```

### Sample Input 2
```
board = [["."]]
```
### Sample Output 2
```
0
```

### Solution
```java
class Solution {
    public int countBattleships(char[][] board) {
        int count = 0;
        int rows = board.length;
        int cols = board[0].length;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // Check if the cell is a starting cell of a battleship
                if (board[i][j] == 'X' &&
                    (i == 0 || board[i - 1][j] == '.') &&
                    (j == 0 || board[i][j - 1] == '.')) {
                    count++;
                }
            }
        }
        return count;
    }
}

```

### Accepted
![Screenshot 2025-01-14 at 8 21 47 AM](https://github.com/user-attachments/assets/add8cd77-34d4-4bdd-9337-756139411c7b)
