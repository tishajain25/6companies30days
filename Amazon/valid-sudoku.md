# Valid Sudoku

[Problem Link](https://leetcode.com/problems/valid-sudoku/description/) 

Given a 9x9 Sudoku board, determine if the board is valid. A board is valid if:

Each row contains unique digits (1-9) without repetition.
Each column contains unique digits (1-9) without repetition.
Each of the nine 3x3 subgrids contains unique digits (1-9) without repetition.
Empty cells are represented by '.' and need not be validated.


### Sample Input 1
```
board = [
    ["5","3",".",".","7",".",".",".","."],
    ["6",".",".","1","9","5",".",".","."],
    [".","9","8",".",".",".",".","6","."],
    ["8",".",".",".","6",".",".",".","3"],
    ["4",".",".","8",".","3",".",".","1"],
    ["7",".",".",".","2",".",".",".","6"],
    [".","6",".",".",".",".","2","8","."],
    [".",".",".","4","1","9",".",".","5"],
    [".",".",".",".","8",".",".","7","9"]
]
```
### Sample Output 1
```
true
```

### Solution
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        // Create three sets to track numbers in rows, columns, and subgrids
        Set<String> rows = new HashSet<>();
        Set<String> cols = new HashSet<>();
        Set<String> subgrids = new HashSet<>();
        
        // Traverse each cell in the 9x9 board
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                char num = board[i][j];
                if (num == '.') {
                    continue; // Skip empty cells
                }
                
                // Create a unique key for the row, column, and subgrid
                String rowKey = "row" + i + num;
                String colKey = "col" + j + num;
                String subgridKey = "subgrid" + (i / 3) + (j / 3) + num;
                
                // Check if the number already exists in the row, column, or subgrid
                if (rows.contains(rowKey) || cols.contains(colKey) || subgrids.contains(subgridKey)) {
                    return false;
                }
                
                // Add the number to the sets
                rows.add(rowKey);
                cols.add(colKey);
                subgrids.add(subgridKey);
            }
        }
        
        // If no violations were found, return true
        return true;
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 10 27 43 PM](https://github.com/user-attachments/assets/df14cf6b-285a-40d5-8e2e-6e6a7dceff27)
