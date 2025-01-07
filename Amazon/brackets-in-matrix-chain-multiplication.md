# Brackets in Matrix Chain Multiplication

[Problem Link](https://www.geeksforgeeks.org/problems/brackets-in-matrix-chain-multiplication1024/1) 

Given an array arr[] of size n, where arr[i] x arr[i+1] represents the dimensions of n-1 matrices, find the optimal order 
of multiplication to minimize scalar multiplications. Return the order as a string with uppercase letters (A-Z) for matrices and 
parentheses () for grouping.


### Sample Input 1
```
arr = [40, 20, 30, 10, 30]  
```
### Sample Output 1
```
((A(BC))D)
```

### Sample Input 2
```
arr = [10, 20, 30]  
```
### Sample Output 2
```
(AB)
```

### Solution
```java
class Solution {
    static String matrixChainOrder(int arr[]) {
        int n = arr.length;
        int[][] dp = new int[n][n];
        int[][] split = new int[n][n];
        String[][] brackets = new String[n][n];

        // Initialize brackets for single matrices
        for (int i = 1; i < n; i++) {
            brackets[i][i] = Character.toString((char) ('A' + i - 1));
        }

        // Fill DP table
        for (int len = 2; len < n; len++) {
            for (int i = 1; i < n - len + 1; i++) {
                int j = i + len - 1;
                dp[i][j] = Integer.MAX_VALUE;

                for (int k = i; k < j; k++) {
                    int cost = dp[i][k] + dp[k + 1][j] + arr[i - 1] * arr[k] * arr[j];
                    if (cost < dp[i][j]) {
                        dp[i][j] = cost;
                        split[i][j] = k;
                        brackets[i][j] = "(" + brackets[i][k] + brackets[k + 1][j] + ")";
                    }
                }
            }
        }

        // Return the bracketed string for the optimal order
        return brackets[1][n - 1];
    }
}
```

### Accepted
![Screenshot 2025-01-07 at 9 50 11 PM](https://github.com/user-attachments/assets/74320b57-82b0-47ec-969b-b380fbc7c4a1)
