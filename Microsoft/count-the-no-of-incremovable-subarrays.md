# Count The Number of Incremovable Subarrays

[Problem Link](https://leetcode.com/problems/count-the-number-of-incremovable-subarrays-i/description/) 

Given an array of positive integers, count the number of incremovable subarrays, where removing the subarray results in a strictly 
increasing array.


### Sample Input
```
nums = [1, 2, 3, 4] 
```
### Sample Output
```
10 
```

### Solution
```java
class Solution {
    public int incremovableSubarrayCount(int[] nums) {
        int n = nums.length;
        int count = 0;

        for (int start = 0; start < n; start++) {
            for (int end = start; end < n; end++) {
                // Extract the subarray to remove
                List<Integer> remaining = new ArrayList<>();
                for (int i = 0; i < n; i++) {
                    if (i < start || i > end) {
                        remaining.add(nums[i]);
                    }
                }

                // Check if the remaining array is strictly increasing
                if (isStrictlyIncreasing(remaining)) {
                    count++;
                }
            }
        }
        return count;
    }

    private static boolean isStrictlyIncreasing(List<Integer> array) {
        for (int i = 1; i < array.size(); i++) {
            if (array.get(i) <= array.get(i - 1)) {
                return false;
            }
        }
        return true;
    }
}
```

### Accepted
![Screenshot 2024-12-31 at 10 29 56 PM](https://github.com/user-attachments/assets/90a0eb9c-2157-4fd5-bf0e-db967cb8f6fc)
