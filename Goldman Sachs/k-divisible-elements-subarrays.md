# K Divisible Elements Subarrays

[Problem Link](https://leetcode.com/problems/k-divisible-elements-subarrays/description/) 


Given an integer array nums and two integers k and p, return the number of distinct subarrays that contain at most k elements divisible by p.

A subarray is any contiguous sequence of elements in the array, and distinct subarrays are those that are different in length or have at least one element that differs in value.

### Sample Input 1
```
nums = [2, 3, 3, 2, 2], k = 2, p = 2
```

### Sample Output 1
```
11
```

### Sample Input 2
```
nums = [1, 2, 3, 4], k = 4, p = 1
```

### Sample Output 2
```
10
```

### Solution
```java
class Solution {
    public int countDistinct(int[] nums, int k, int p) {
      Set<String> distinctSubarrays = new HashSet<>();
        int n = nums.length;

        // Iterate over all possible starting points for subarrays
        for (int i = 0; i < n; i++) {
            int countDivisible = 0;
            StringBuilder subarray = new StringBuilder();

            // Iterate over all possible ending points for subarrays
            for (int j = i; j < n; j++) {
                if (nums[j] % p == 0) {
                    countDivisible++;
                }
                
                // If the count of divisible elements exceeds k, stop considering further subarrays
                if (countDivisible > k) {
                    break;
                }

                // Build the subarray and add it to the set
                subarray.append(nums[j]).append(",");
                distinctSubarrays.add(subarray.toString());
            }
        }

        // Return the size of the set which gives the number of distinct subarrays
        return distinctSubarrays.size();
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 17 04 PM](https://github.com/user-attachments/assets/6d3240f3-cf0a-48cc-88bd-e435e20f028c)
