# Count Number of Nice Subarrays

[Problem Link](https://leetcode.com/problems/count-number-of-nice-subarrays/description/) 

You are given an array of integers nums and an integer k. You need to find the number of subarrays that contain exactly k 
odd numbers. A subarray is a contiguous part of the array.


### Sample Input 
```
nums = [2, 2, 2, 1, 2, 2, 1, 2, 2, 2], k = 2
```
### Sample Output 
```
16
```


### Solution
```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        // Helper function to count subarrays with at most 'k' odd numbers
        return atMostK(nums, k) - atMostK(nums, k - 1);
    }

    private int atMostK(int[] nums, int k) {
        int count = 0, left = 0, result = 0;

        for (int right = 0; right < nums.length; right++) {
            // If the number is odd, decrease k
            if (nums[right] % 2 != 0) {
                k--;
            }

            // If k < 0, move the left pointer to restore k
            while (k < 0) {
                if (nums[left] % 2 != 0) {
                    k++;
                }
                left++;
            }

            // Count subarrays ending at 'right'
            result += right - left + 1;
        }

        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-02 at 9 45 06 PM](https://github.com/user-attachments/assets/4560f753-e8af-45db-9ff6-84b72cd89d6a)
