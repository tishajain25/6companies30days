# Longest Mountain in Array

[Problem Link](https://leetcode.com/problems/longest-mountain-in-array/) 

Given an integer array arr, return the length of the longest subarray that forms a "mountain." A mountain is defined as a subarray 
where the elements first strictly increase to a peak and then strictly decrease. The subarray must have at least 3 elements, and the 
peak must be greater than its neighbors. If no mountain exists, return 0.


### Sample Input 1
```
arr = [2,1,4,7,3,2,5]
```
### Sample Output 1
```
5
```

### Sample Input 2
```
arr = [2,2,2]
```
### Sample Output 2
```
0
```

### Solution
```java
class Solution {
    public int longestMountain(int[] arr) {
        int n = arr.length;
        int maxLength = 0;

        // Traverse the array
        for (int i = 1; i < n - 1; i++) {
            // Check if arr[i] is the peak of a mountain
            if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
                int left = i - 1;
                int right = i + 1;

                // Expand left while the array is strictly increasing
                while (left >= 0 && arr[left] < arr[left + 1]) {
                    left--;
                }

                // Expand right while the array is strictly decreasing
                while (right < n && arr[right] < arr[right - 1]) {
                    right++;
                }

                // Calculate the length of the current mountain
                maxLength = Math.max(maxLength, right - left - 1);
            }
        }
        return maxLength;
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 10 13 00 PM](https://github.com/user-attachments/assets/9d4f0200-acc1-4142-ab15-adbf08b753fa)
