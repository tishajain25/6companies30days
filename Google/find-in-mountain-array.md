# Find in Mountain Array

[Problem Link](https://leetcode.com/problems/find-in-mountain-array/description/) 

You are given a Mountain Array (an array that first strictly increases, then strictly decreases) and a target value. Your task is to find the smallest index where the value equals target. If target is not present, return -1.

You can only interact with the array through the MountainArray interface:

1. MountainArray.get(index): Returns the value at index.
2. MountainArray.length(): Returns the length of the array.

You must minimize the number of calls to MountainArray.get, with a limit of 100 calls.

### Sample Input 1
```
mountainArr = [1,2,3,4,5,3,1], target = 3
```
### Sample Output 1
```
2
```

### Sample Input 2
```
mountainArr = [0,1,2,4,2,1], target = 3
```
### Sample Output 2
```
-1
```

### Solution
```java
class Solution {
    public int findInMountainArray(int target, MountainArray mountainArr) {
        int n = mountainArr.length();
        
        // Step 1: Find the peak index
        int peak = findPeak(mountainArr, n);
        
        // Step 2: Search in the ascending part
        int index = binarySearch(mountainArr, target, 0, peak, true);
        if (index != -1) return index;
        
        // Step 3: Search in the descending part
        return binarySearch(mountainArr, target, peak + 1, n - 1, false);
    }
    
    private int findPeak(MountainArray mountainArr, int n) {
        int left = 0, right = n - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (mountainArr.get(mid) < mountainArr.get(mid + 1)) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left; // Peak index
    }
    
    private int binarySearch(MountainArray mountainArr, int target, int left, int right, boolean ascending) {
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int midVal = mountainArr.get(mid);
            
            if (midVal == target) return mid;
            
            if (ascending) {
                if (midVal < target) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            } else {
                if (midVal > target) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1; // Target not found
    }
}
```

### Accepted
![Screenshot 2025-01-19 at 3 24 32 PM](https://github.com/user-attachments/assets/6f88fea8-9f80-45b1-abae-3b52ce21f82e)
