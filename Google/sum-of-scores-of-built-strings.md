# Sum of Scores of Built Strings

[Problem Link](https://leetcode.com/problems/sum-of-scores-of-built-strings/description/) 

Given a string s, calculate the sum of scores for all suffixes of s. The score of a suffix s[i:] is the length of the longest common 
prefix between s[i:] and s. Return the total score.

### Sample Input 1
```
s = "babab"
```
### Sample Output 1
```
9
```

### Sample Input 2
```
s = "azbazbzaz"
```
### Sample Output 2
```
14
```

### Solution
```java
class Solution {
    public long sumScores(String s) {
      int n = s.length();
        int[] z = computeZArray(s); // Compute Z-array
        long totalScore = 0;

        for (int value : z) {
            totalScore += value; // Sum up all Z-values
        }

        return totalScore;
    }

    // Z-algorithm to compute Z-array
    private int[] computeZArray(String s) {
        int n = s.length();
        int[] z = new int[n];
        int l = 0, r = 0;

        for (int i = 1; i < n; i++) {
            if (i <= r) {
                z[i] = Math.min(r - i + 1, z[i - l]);
            }
            while (i + z[i] < n && s.charAt(z[i]) == s.charAt(i + z[i])) {
                z[i]++;
            }
            if (i + z[i] - 1 > r) {
                l = i;
                r = i + z[i] - 1;
            }
        }

        // Include the full string as a prefix
        z[0] = n;
        return z;
    }
}
```

### Accepted
![Screenshot 2025-01-17 at 1 37 50 PM](https://github.com/user-attachments/assets/71d27675-254a-4a99-b745-51f61d7cc7d0)
