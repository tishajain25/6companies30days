# Random Flip Matrix

[Problem Link](https://leetcode.com/problems/random-flip-matrix/description/) 


You are given a binary matrix of size m x n, where all values are initially set to 0. You need to design a system that can perform the following operations:

flip(): Randomly pick an index (i, j) where matrix[i][j] == 0 and flip it to 1. All unflipped cells (cells with value 0) should have an equal chance of being selected.

reset(): Resets the matrix to all 0s.

You need to optimize the algorithm to minimize the number of calls to the built-in random function and also optimize for time and space complexity.



Return a list of all valid combinations.

### Sample Input 
```
["Solution", "flip", "flip", "flip", "reset", "flip"]
[[3, 1], [], [], [], [], []]
```

### Sample Output 
```
[null, [1, 0], [2, 0], [0, 0], null, [2, 0]]
```

### Solution
```java
class Solution {

    public Solution(int n_rows, int n_cols) {
        this.rows = n_rows;
        this.cols = n_cols;
        this.total = n_rows * n_cols;
    }

    public int[] flip() {
        // All the candidates are used out.
        if (used.size() == total)
            return new int[] {};
        int index = new Random().nextInt(total);
        while (used.contains(index))
            index = ++index % total;
        used.add(index);
        return new int[] {index / cols, index % cols};
    }

    public void reset() {
        used.clear();
    }

    private Set<Integer> used = new HashSet<>();
    private int rows;
    private int cols;
    private int total;
}
```

### Accepted
![Screenshot 2025-01-24 at 4 01 35 PM](https://github.com/user-attachments/assets/14deadd9-0e32-4230-9bad-25be99966ed0)
