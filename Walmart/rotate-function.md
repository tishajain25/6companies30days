# Rotate Function

[Problem Link](https://leetcode.com/problems/rotate-function/description/) 

You are given an integer array nums of length n. Define a rotation function F(k) as:
F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1]
where arr k is the array obtained by rotating nums k times clockwise.
Find the maximum value of F(k) for k=0 to n−1.


### Sample Input 1
```
nums = [4,3,2,6]
```
### Sample Output 1
```
26
```

### Sample Input 2
```
nums = [100]
```
### Sample Output 2
```
0
```

### Solution
```java
class Solution {
    public int maxRotateFunction(int[] nums) {
       int n = nums.length;
        int sum = 0; // Sum of all elements in nums
        int F = 0;   // Initial value of F(0)
        
        // Calculate sum of nums and F(0)
        for (int i = 0; i < n; i++) {
            sum += nums[i];
            F += i * nums[i];
        }
        
        int maxF = F; // Initialize maxF with F(0)
        
        // Use the relationship to calculate F(k) for k = 1 to n-1
        for (int k = 1; k < n; k++) {
            F = F + sum - n * nums[n - k];
            maxF = Math.max(maxF, F);
        }
        
        return maxF;
    }
}
```

### Accepted
![Screenshot 2025-01-12 at 12 18 11 PM](https://github.com/user-attachments/assets/1b5b06a1-b0a8-415f-9b85-668b2a934a61)
