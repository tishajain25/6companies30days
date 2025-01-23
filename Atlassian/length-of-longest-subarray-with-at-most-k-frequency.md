# Length of Longest Subarray With at Most K Frequency

[Problem Link](https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/description/) 

Given an integer array nums and an integer k, find the length of the longest subarray where the frequency of each element is at most 
k. A subarray is a contiguous part of the array.


Return the distance value between the two arrays.

### Sample Input 1
```
nums = [1, 2, 3, 1, 2, 3, 1, 2]
k = 2
```
### Sample Output 1
```
6
```

### Sample Input 2
```
nums = [1, 2, 1, 2, 1, 2, 1, 2]
k = 1
```
### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    public int maxSubarrayLength(int[] nums, int k) {
      HashMap<Integer, Integer> freqMap = new HashMap<>();
        int left = 0, maxLength = 0;

        for (int right = 0; right < nums.length; right++) {
            // Add the current element to the frequency map
            freqMap.put(nums[right], freqMap.getOrDefault(nums[right], 0) + 1);

            // Check if the current window is invalid
            while (freqMap.get(nums[right]) > k) {
                // Shrink the window from the left
                freqMap.put(nums[left], freqMap.get(nums[left]) - 1);
                if (freqMap.get(nums[left]) == 0) {
                    freqMap.remove(nums[left]);
                }
                left++;
            }

            // Update the maximum length
            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }
}
```

### Accepted
![Screenshot 2025-01-23 at 12 18 40 PM](https://github.com/user-attachments/assets/479b7da6-80b3-4848-a36e-349120c57874)
