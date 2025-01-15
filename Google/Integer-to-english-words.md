# Integer to English Words

[Problem Link](https://leetcode.com/problems/integer-to-english-words/description/) 

Convert a non-negative integer num to its English words representation.

### Sample Input 1
```
num = 123
```
### Sample Output 1
```
"One Hundred Twenty Three"
```

### Sample Input 2
```
num = 12345
```
### Sample Output 2
```
"Twelve Thousand Three Hundred Forty Five"
```

### Solution
```java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
       // Step 1: Initialize the distance matrix
        int[][] dist = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], Integer.MAX_VALUE / 2); // Use a large value to represent infinity
            dist[i][i] = 0; // Distance to itself is 0
        }

        // Step 2: Fill the distance matrix with given edges
        for (int[] edge : edges) {
            int from = edge[0], to = edge[1], weight = edge[2];
            dist[from][to] = weight;
            dist[to][from] = weight; // Since the graph is bidirectional
        }

        // Step 3: Floyd-Warshall Algorithm to calculate shortest distances
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }

        // Step 4: Find the city with the smallest number of reachable cities
        int minCount = Integer.MAX_VALUE;
        int resultCity = -1;

        for (int i = 0; i < n; i++) {
            int reachableCount = 0;

            // Count cities reachable within the distanceThreshold
            for (int j = 0; j < n; j++) {
                if (dist[i][j] <= distanceThreshold) {
                    reachableCount++;
                }
            }

            // Update the result city
            if (reachableCount <= minCount) {
                minCount = reachableCount;
                resultCity = i; // Choose the city with the larger index in case of a tie
            }
        }

        return resultCity;
    }
}
```

### Accepted
![Screenshot 2025-01-15 at 8 56 57 PM](https://github.com/user-attachments/assets/16fc5eb8-998e-48fa-b6d4-571f873348d8)
