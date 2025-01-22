# Find the City With the Smallest Number of Neighbors at a Threshold Distance

[Problem Link](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/description/) 

You are given n cities connected by bidirectional roads with specific weights. For each city, determine how many cities are reachable within a given distance threshold. 
Return the city with the smallest number of reachable cities. If there is a tie, return the city with the largest number.

### Sample Input 1
```
n = 4,
edges = [[0,1,3],[1,2,1],[1,3,4],[2,3,1]],
distanceThreshold = 4
```
### Sample Output 1
```
3
```

### Sample Input 2
```
n = 5,
edges = [[0,1,2],[0,4,8],[1,2,3],[1,4,2],[2,3,1],[3,4,1]],
distanceThreshold = 2
```
### Sample Output 2
```
0
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
![Screenshot 2025-01-15 at 8 52 04 PM](https://github.com/user-attachments/assets/0ad7f324-88ce-4eb9-a171-1acc6c07ddcf)
