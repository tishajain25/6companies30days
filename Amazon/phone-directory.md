# Phone Directory

[Problem Link](https://www.geeksforgeeks.org/problems/phone-directory4628/1) 

Given a list of n contacts and a query string s, return the list of contacts that match each prefix of s (from the first character 
to the full string) in lexicographical order. If no contacts match a prefix, return "0" for that prefix.


### Sample Input 
```
n = 3  
contacts = ["geeikistest", "geeksforgeeks", "geeksfortest"]  
s = "geeips" 
```
### Sample Output 
```
geeikistest geeksforgeeks geeksfortest  
geeikistest geeksforgeeks geeksfortest  
geeikistest geeksforgeeks geeksfortest  
geeikistest  
0  
0
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
![Screenshot 2025-01-07 at 9 59 29 PM](https://github.com/user-attachments/assets/98eff583-4c61-47c2-869c-a24b4cd9388c)
