# Best Time to Buy and Sell Stock IV

[Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/) 

Given an array prices where prices[i] is the price of a stock on the ith day, and an integer k (maximum transactions allowed), 
determine the maximum profit you can achieve by completing at most k transactions. A transaction consists of buying and selling the 
stock once, and you cannot hold multiple stocks at the same time.


### Sample Input 1
```
k = 2, prices = [2,4,1]  
```
### Sample Output 1
```
2
```

### Sample Input 2
```
k = 2, prices = [3,2,6,5,0,3]  
```
### Sample Output 2
```
7
```

### Solution
```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        int n = prices.length;
        if (n == 0 || k == 0) return 0;

        // If k >= n/2, it means we can perform unlimited transactions
        if (k >= n / 2) {
            int maxProfit = 0;
            for (int i = 1; i < n; i++) {
                if (prices[i] > prices[i - 1]) {
                    maxProfit += prices[i] - prices[i - 1];
                }
            }
            return maxProfit;
        }

        // DP table
        int[][] dp = new int[k + 1][n];
        
        for (int i = 1; i <= k; i++) {
            int maxDiff = -prices[0]; // Tracks the max profit for buying
            for (int j = 1; j < n; j++) {
                dp[i][j] = Math.max(dp[i][j - 1], prices[j] + maxDiff);
                maxDiff = Math.max(maxDiff, dp[i - 1][j] - prices[j]);
            }
        }

        return dp[k][n - 1];
    }
}
```

### Accepted
![Screenshot 2025-01-07 at 9 44 54 PM](https://github.com/user-attachments/assets/72202d89-c785-44a4-bd76-bbc1bc2b0dc7)
