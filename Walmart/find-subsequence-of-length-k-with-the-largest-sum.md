# Find Subsequence of Length K With the Largest Sum

[Problem Link](https://leetcode.com/problems/get-equal-substrings-within-budget/description/) 

Given an integer array nums and an integer k, find a subsequence of length k that has the largest sum. The subsequence must retain the order of 
elements as in the original array. If multiple solutions exist, return any.

### Sample Input 1
```
nums = [2,1,3,3], k = 2
```
### Sample Output 1
```
[3,3]
```

### Sample Input 2
```
nums = [-1,-2,3,4], k = 3
```
### Sample Output 2
```
[-1,3,4]
```

### Solution
```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        // Pair each number with its index
        int[][] pairs = new int[nums.length][2];
        for (int i = 0; i < nums.length; i++) {
            pairs[i][0] = nums[i];
            pairs[i][1] = i;
        }

        // Sort by values in descending order
        Arrays.sort(pairs, (a, b) -> b[0] - a[0]);

        // Select the top k elements
        int[][] selected = Arrays.copyOfRange(pairs, 0, k);

        // Sort the selected elements by their original indices
        Arrays.sort(selected, Comparator.comparingInt(a -> a[1]));

        // Extract the values to form the result
        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = selected[i][0];
        }

        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-11 at 10 06 21 PM](https://github.com/user-attachments/assets/8c34d9a6-685b-467b-a33b-1f28bae6856c)

