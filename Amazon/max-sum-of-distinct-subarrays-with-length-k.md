# Maximum Sum of Distinct Subarrays with Length K

[Problem Link](https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/description/) 

You are given an integer array nums and an integer k. Your task is to find the maximum sum of any subarray of length k that 
contains only distinct elements. If no such subarray exists, return 0.


### Sample Input 1
```
nums = [1,5,4,2,9,9,9], k = 3
```
### Sample Output 1
```
15
```

### Solution
```java
class Solution {
    public long maximumSubarraySum(int[] nums, int k) {
        long ans = 0;
    long sum = 0;
    int distinct = 0;
    Map<Integer, Integer> count = new HashMap<>();

    for (int i = 0; i < nums.length; ++i) {
        sum += nums[i];
        if (count.merge(nums[i], 1, Integer::sum) == 1)
        ++distinct;
        if (i >= k) {
            if (count.merge(nums[i - k], -1, Integer::sum) == 0)
                --distinct;
            sum -= nums[i - k];
      }
      if (i >= k - 1 && distinct == k)
        ans = Math.max(ans, sum);
    }

    return ans;
  }
}
```

### Accepted
![Screenshot 2025-01-05 at 10 23 01 PM](https://github.com/user-attachments/assets/8577e038-e787-4f86-84b8-19b93b67b8f0)
