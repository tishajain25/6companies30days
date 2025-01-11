# K-diff Pairs in an Array

[Problem Link](https://leetcode.com/problems/k-diff-pairs-in-an-array/description/) 

Given an array of integers nums and an integer k, find the number of unique k-diff pairs in the array. 
A k-diff pair is a pair of integers (nums[i], nums[j]) where |nums[i] - nums[j]| == k and i != j.


### Sample Input 1
```
nums = [3,1,4,1,5], k = 2
```
### Sample Output 1
```
2
```

### Sample Input 2
```
nums = [1,2,3,4,5], k = 1
```
### Sample Output 2
```
4
```

### Solution
```java
class Solution {
    public int findPairs(int[] nums, int k) {
        if (k < 0) return 0; // Difference cannot be negative
        
        HashMap<Integer, Integer> map = new HashMap<>();
        int count = 0;

        // Count frequency of each number
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        for (int key : map.keySet()) {
            if (k == 0) {
                // For k = 0, check if there are duplicates
                if (map.get(key) > 1) {
                    count++;
                }
            } else {
                // For k > 0, check if key + k exists
                if (map.containsKey(key + k)) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

### Accepted
![Screenshot 2025-01-11 at 10 24 52 PM](https://github.com/user-attachments/assets/d073fbd4-f21d-4108-bc1d-71efbd8e98e2)
