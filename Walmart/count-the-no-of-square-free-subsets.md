# Count the Number of Square-Free Subsets

[Problem Link](https://leetcode.com/problems/count-the-number-of-square-free-subsets/description/)

Given an array of integers nums, return the number of non-empty subsets of nums such that the product of the elements in each subset 
is a square-free integer. A square-free integer is one that is not divisible by any perfect square other than 1.


### Sample Input 1
```
nums = [3, 4, 4, 5]
```
### Sample Output 1
```
3
```

### Sample Input 2
```
nums = [1]
```
### Sample Output 2
```
1
```

### Solution
```java
class Solution {
    public int squareFreeSubsets(int[] nums) {
        Integer[][] mem = new Integer[nums.length][1 << (kPrimesCount + 1)];
        int[] masks = new int[nums.length];

        for (int i = 0; i < nums.length; ++i)
            masks[i] = getMask(nums[i]);

        // -1 means that we take no number.
        // `used` is initialized to 1 so that -1 & 1 = 1 instead of 0.
        return (squareFreeSubsets(masks, 0, /*used=*/1, mem) - 1 + kMod) % kMod;
    }

    private static final int kMod = 1_000_000_007;
    private static final int kPrimesCount = 10;
    private static final int[] primes = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29};

    private int squareFreeSubsets(int[] masks, int i, int used, Integer[][] mem) {
        if (i == masks.length)
            return 1;
        if (mem[i][used] != null)
            return mem[i][used];
        final int pick =
        (masks[i] & used) == 0 ? squareFreeSubsets(masks, i + 1, used | masks[i], mem) : 0;
        final int skip = squareFreeSubsets(masks, i + 1, used, mem);
        return mem[i][used] = (pick + skip) % kMod;
    }

    // e.g. num = 10 = 2 * 5, so mask = 0b101 -> 0b1010 (append a 0)
    //      num = 15 = 3 * 5, so mask = 0b110 -> 0b1100 (append a 0)
    //      num = 25 = 5 * 5, so mask =  0b-1 -> 0b1..1 (invalid)
    private int getMask(int num) {
        int mask = 0;
        for (int i = 0; i < primes.length; ++i) {
            int rootCount = 0;
            while (num % primes[i] == 0) {
                num /= primes[i];
                ++rootCount;
            }
            if (rootCount >= 2)
                return -1;
            if (rootCount == 1)
                mask |= 1 << i;
        }
        return mask << 1;
    }
}
```

### Accepted
![Screenshot 2025-01-11 at 10 37 56 PM](https://github.com/user-attachments/assets/0a80d2f0-a69e-4d7e-b0e1-10478a4a6b2d)
