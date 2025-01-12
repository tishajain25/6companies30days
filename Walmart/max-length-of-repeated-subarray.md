# Maximum Length of Repeated Subarray

[Problem Link](https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/) 

Given two integer arrays nums1 and nums2, find the maximum length of a contiguous subarray that appears in both arrays.


### Sample Input 1
```
nums1 = [1,2,3,2,1]
nums2 = [3,2,1,4,7]
```
### Sample Output 1
```
3
```

### Sample Input 2
```
nums1 = [0,0,0,0,0]
nums2 = [0,0,0,0,0]
```
### Sample Output 2
```
5
```

### Solution
```java
class Solution {
    public int findLength(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        int[][] dp = new int[m + 1][n + 1]; // DP table
        int maxLength = 0;

        // Build the DP table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (nums1[i - 1] == nums2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1; // Extend the common subarray
                    maxLength = Math.max(maxLength, dp[i][j]); // Update max length
                }
            }
        }

        return maxLength;
    }
}
```

### Accepted
![Screenshot 2025-01-12 at 12 31 22 PM](https://github.com/user-attachments/assets/feb8c444-d36d-4f1a-875b-62d7a132ec22)
