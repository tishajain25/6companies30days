# Minimum Cost to Convert String I

[Problem Link](https://leetcode.com/problems/minimum-cost-to-convert-string-i/) 

You are given two strings, source and target, of equal length, and arrays original, changed, and cost. Each transformation from 
original[i] to changed[i] costs cost[i]. You can repeatedly transform characters in source to make it identical to target. 
Return the minimum cost to achieve this transformation, or -1 if it's impossible.

### Sample Input 
```
source = "abcd"
target = "acbe"
original = ['a', 'b', 'c', 'c', 'e', 'd']
changed = ['b', 'c', 'b', 'e', 'b', 'e']
cost = [2, 5, 5, 1, 2, 20]
```
### Sample Output 
```
28
```

### Solution
```java
class Solution {
    public long minimumCost(String source, String target, char[] original, char[] changed, int[] cost) {
         // Define a very large value to represent "infinity" for unreachable transformations
        final int inf = 1 << 29;

        // Create a 26x26 matrix to store the minimum cost of transforming one character to another
        int[][] g = new int[26][26];

        // Initialize the transformation cost matrix
        for (int i = 0; i < 26; ++i) {
            Arrays.fill(g[i], inf); // Initially, set all transformation costs to "infinity"
            g[i][i] = 0;            // The cost to transform a character to itself is 0
        }

        // Populate the transformation costs using the given `original`, `changed`, and `cost` arrays
        for (int i = 0; i < original.length; ++i) {
            int x = original[i] - 'a';  // Convert the `original` character to its index (0-25)
            int y = changed[i] - 'a';   // Convert the `changed` character to its index (0-25)
            int z = cost[i];            // The cost of transforming `original[i]` to `changed[i]`
            g[x][y] = Math.min(g[x][y], z); // Store the minimum cost for this transformation
        }

        // Use Floyd-Warshall algorithm to compute the shortest transformation cost between all pairs of characters
        for (int k = 0; k < 26; ++k) {       // Intermediate character
            for (int i = 0; i < 26; ++i) {   // Starting character
                for (int j = 0; j < 26; ++j) { // Target character
                    // Update the cost of transforming `i` to `j` via `k`
                    g[i][j] = Math.min(g[i][j], g[i][k] + g[k][j]);
                }
            }
        }

        // Initialize the total cost to 0
        long ans = 0;

        // Iterate through each character in the `source` and `target` strings
        int n = source.length();
        for (int i = 0; i < n; ++i) {
            int x = source.charAt(i) - 'a';  // Get the index of the current character in `source`
            int y = target.charAt(i) - 'a';  // Get the index of the corresponding character in `target`

            if (x != y) { // If the characters are different, we need to transform `x` to `y`
                if (g[x][y] >= inf) { // If the transformation is impossible (cost is "infinity")
                    return -1;        // Return -1 as the transformation cannot be completed
                }
                ans += g[x][y]; // Add the cost of transforming `x` to `y` to the total cost
            }
        }

        // Return the total cost of transforming the entire `source` string to the `target` string
        return ans;
    }
}
```

### Accepted
![Screenshot 2025-01-03 at 10 43 56 PM](https://github.com/user-attachments/assets/31e92f37-ca22-4ed6-be85-e288e52b2afa)
