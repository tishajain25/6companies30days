# Largest Divisible Subset

[Problem Link](https://leetcode.com/problems/largest-divisible-subset/description/) 

Given a list of distinct positive integers, find the largest subset such that for every pair of numbers in the subset, one is divisible by the other. 
If multiple solutions exist, return any.

### Sample Input 1
```
nums = [1, 2, 3]  
```
### Sample Output 1
```
[1, 2]
```

### Sample Input 2
```
nums = [1, 2, 4, 8]  
```
### Sample Output 2
```
[1, 2, 4, 8]
```

### Solution
```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        // Step 1: Sort the array
        Arrays.sort(nums);

        int n = nums.length;
        int[] dp = new int[n]; // dp[i] stores the size of the largest subset ending at index i
        int[] parent = new int[n]; // parent[i] stores the previous index in the subset
        Arrays.fill(dp, 1);
        Arrays.fill(parent, -1);

        int maxSize = 0, maxIndex = -1;

        // Step 2: Build the DP table
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] % nums[j] == 0 && dp[i] < dp[j] + 1) {
                    dp[i] = dp[j] + 1;
                    parent[i] = j;
                }
            }
            if (dp[i] > maxSize) {
                maxSize = dp[i];
                maxIndex = i;
            }
        }

        // Step 3: Reconstruct the subset
        List<Integer> result = new ArrayList<>();
        while (maxIndex != -1) {
            result.add(nums[maxIndex]);
            maxIndex = parent[maxIndex];
        }

        Collections.reverse(result);
        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-11 at 9 56 40 PM](https://github.com/user-attachments/assets/14e49c34-5466-4824-924c-7d939bf0dc55)

