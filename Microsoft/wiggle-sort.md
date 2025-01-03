# Wiggle Sort II

[Problem Link](https://leetcode.com/problems/wiggle-sort-ii/) 

Rearrange an array nums such that it follows the pattern:
nums[0] < nums[1] > nums[2] < nums[3]...

You must reorder the array in-place to achieve this wiggle pattern. The input array is guaranteed to have a valid solution.

### Sample Input 
```
nums = [1, 5, 1, 1, 6, 4] 
```
### Sample Output 
```
[1, 6, 1, 5, 1, 4]  
```

### Solution
```java
class Solution {
    public void wiggleSort(int[] nums) {
        int n = nums.length;

        // Step 1: Find the median
        int[] sorted = nums.clone();
        Arrays.sort(sorted);
        int median = sorted[(n - 1) / 2];

        // Step 2: Virtual Indexing
        int left = 0, i = 0, right = n - 1;

        while (i <= right) {
            if (nums[mapIndex(i, n)] > median) {
                swap(nums, mapIndex(left++, n), mapIndex(i++, n));
            } else if (nums[mapIndex(i, n)] < median) {
                swap(nums, mapIndex(i, n), mapIndex(right--, n));
            } else {
                i++;
            }
        }
    }

    // Virtual index mapping
    private int mapIndex(int index, int n) {
        return (1 + 2 * index) % (n | 1);
    }

    // Swap helper function
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

### Accepted
![Screenshot 2025-01-03 at 10 04 07 PM](https://github.com/user-attachments/assets/4d8bf7e1-9e5f-43ef-b34a-3c4bd08e7d62)
