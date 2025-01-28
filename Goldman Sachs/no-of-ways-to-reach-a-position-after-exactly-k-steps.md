# Number of Ways to Reach a Position After Exactly k Steps

[Problem Link](https://leetcode.com/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps/description/)

You are standing at position startPos on an infinite number line and need to reach endPos in exactly k steps. Each step lets you move 
either one position left or right. Return the number of different ways to achieve this, modulo 10^9 +7. If it's not possible, return 0.

### Sample Input 
```
startPos = 1, endPos = 2, k = 3
```

### Sample Output 
```
3
```

### Solution
```java
class Solution {
    private Integer[][] f;
    private final int mod = (int) 1e9 + 7;

    public int numberOfWays(int startPos, int endPos, int k) {
        f = new Integer[k + 1][k + 1];
        return dfs(Math.abs(startPos - endPos), k);
    }

    private int dfs(int i, int j) {
        if (i > j || j < 0) {
            return 0;
        }
        if (j == 0) {
            return i == 0 ? 1 : 0;
        }
        if (f[i][j] != null) {
            return f[i][j];
        }
        int ans = dfs(i + 1, j - 1) + dfs(Math.abs(i - 1), j - 1);
        ans %= mod;
        return f[i][j] = ans;
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 9 07 34 PM](https://github.com/user-attachments/assets/3c996395-e28e-43c0-a993-1b9f798a403b)
