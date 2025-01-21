# Assign Cookies

[Problem Link](https://leetcode.com/problems/assign-cookies/description/) 

You are given two arrays:

1. g[] (children's greed factors) - the minimum cookie size each child needs to be happy.
2. s[] (cookie sizes) - the sizes of cookies available.
   
Each child can have at most one cookie, and a cookie can satisfy a child only if its size is greater than or equal to the child's greed factor.

Your task is to maximize the number of happy children and return this number.
### Sample Input 1
```
g = [1, 2, 3], s = [1, 1]
```
### Sample Output 1
```
1
```

### Sample Input 2
```
g = [1, 2], s = [1, 2, 3]
```
### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        // Sort greed factors and cookie sizes
        Arrays.sort(g);
        Arrays.sort(s);
        
        int childIndex = 0; // Pointer for children
        int cookieIndex = 0; // Pointer for cookies
        
        // Iterate while there are children and cookies available
        while (childIndex < g.length && cookieIndex < s.length) {
            // If the current cookie satisfies the current child's greed
            if (s[cookieIndex] >= g[childIndex]) {
                childIndex++; // Move to the next child
            }
            cookieIndex++; // Move to the next cookie
        }
        
        return childIndex; // Number of content children
    }
}
```

### Accepted
![Screenshot 2025-01-21 at 6 29 33 PM](https://github.com/user-attachments/assets/06981db7-24d4-4a01-afba-362607bdf6e8)
