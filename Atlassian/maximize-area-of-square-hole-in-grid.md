# Maximize Area of Square Hole in Grid

[Problem Link](https://leetcode.com/problems/maximize-area-of-square-hole-in-grid/description/) 

Given a grid formed by n+2 horizontal bars and m+2 vertical bars, some bars can be removed. Your task is to maximize the area of a square hole in the grid by removing some of the 
specified bars. The "hole" is the largest square that can be formed between the remaining bars.

### Sample Input 1
```
n = 2, m = 1  
hBars = [2, 3]  
vBars = [2]  
```
### Sample Output 1
```
4
```

### Sample Input 2
```
n = 1, m = 1  
hBars = [2]  
vBars = [2]  
```
### Sample Output 2
```
4
```

### Solution
```java
class Solution {
    public int maximizeSquareHoleArea(int n, int m, int[] hBars, int[] vBars) {
     int x = Math.min(f(hBars), f(vBars));
        return x * x;
    }

    private int f(int[] nums) {
        Arrays.sort(nums);
        int ans = 1, cnt = 1;
        for (int i = 1; i < nums.length; ++i) {
            if (nums[i] == nums[i - 1] + 1) {
                ans = Math.max(ans, ++cnt);
            } else {
                cnt = 1;
            }
        }
        return ans + 1;
    }
}
```

### Accepted
![Screenshot 2025-01-22 at 11 40 21 AM](https://github.com/user-attachments/assets/3803731c-51d0-4104-bf00-45b145b44b26)
