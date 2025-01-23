# Find the Distance Value Between Two Arrays

[Problem Link](https://leetcode.com/problems/find-the-distance-value-between-two-arrays/description/) 

You are given two integer arrays, arr1 and arr2, and an integer d. A "distance value" is defined as the count of elements in arr1 such that 
for every element in arr2, the condition ∣arr1[i] − arr2[j]∣ > d holds.

Return the distance value between the two arrays.

### Sample Input 1
```
arr1 = [4, 5, 8]
arr2 = [10, 9, 1, 8]
d = 2
```
### Sample Output 1
```
2
```

### Sample Input 2
```
arr1 = [1, 4, 2, 3]
arr2 = [-4, -3, 6, 10, 20, 30]
d = 3
```
### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    public int findTheDistanceValue(int[] arr1, int[] arr2, int d) {
    // Sort the second array
        Arrays.sort(arr2);
        int count = 0;

        for (int num : arr1) {
            if (isFarEnough(num, arr2, d)) {
                count++;
            }
        }
        return count;
    }

    private boolean isFarEnough(int num, int[] arr2, int d) {
        int left = 0, right = arr2.length - 1;

        // Binary search for the closest value in arr2
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (Math.abs(num - arr2[mid]) <= d) {
                return false; // Not far enough
            } else if (arr2[mid] < num) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return true; // Far enough
    }
}
```

### Accepted
![Screenshot 2025-01-23 at 12 14 40 PM](https://github.com/user-attachments/assets/1e4ee838-a7c1-4e09-babb-098d3771eb9f)
