# Russian Doll Envelopes

[Problem Link](https://leetcode.com/problems/russian-doll-envelopes/description/) 

You are given an array of integers. Your task is to find the length of the Longest Increasing Subsequence (LIS) in the array. 
A subsequence is derived by deleting some or no elements without changing the order of the remaining elements. The LIS is the 
longest subsequence where each element is strictly greater than the previous one.

### Sample Input 1
```
arr = [10, 9, 2, 5, 3, 7, 101, 18]
```
### Sample Output 1
```
4
```

### Sample Input 2
```
arr = [3, 10, 2, 1, 20]
```
### Sample Output 2
```
3
```

### Solution
```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        // Step 1: Sort envelopes
        Arrays.sort(envelopes, (a, b) -> {
            if (a[0] == b[0]) {
                return b[1] - a[1]; // Sort by height in descending order if widths are the same
            }
            return a[0] - b[0]; // Sort by width in ascending order
        });

        // Step 2: Find LIS based on heights
        int[] dp = new int[envelopes.length];
        int length = 0;

        for (int[] envelope : envelopes) {
            int height = envelope[1];
            int index = Arrays.binarySearch(dp, 0, length, height);
            if (index < 0) {
                index = -(index + 1); // Find the correct position to replace
            }
            dp[index] = height;
            if (index == length) {
                length++;
            }
        }

        return length;
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 9 04 19 PM](https://github.com/user-attachments/assets/d3985010-8b54-425c-8377-49cf247c927d)
