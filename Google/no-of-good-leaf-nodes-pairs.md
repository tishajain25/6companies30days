# Number of Good Leaf Nodes Pairs

[Problem Link](https://leetcode.com/problems/number-of-good-leaf-nodes-pairs/description/) 

Design a data structure that supports adding words and searching for words. The search word may include the wildcard . that matches any single letter.

### Sample Input 
```
root = [1,2,3,null,4], distance = 3
```
### Sample Output 
```
1
```


### Solution
```java
class Solution {
    public int countPairs(TreeNode root, int distance) {
     int[] result = new int[1]; // To store the count of good pairs
        dfs(root, distance, result);
        return result[0];
    }

    private int[] dfs(TreeNode node, int distance, int[] result) {
        if (node == null) return new int[distance + 1]; // Return an empty distance array
        
        // If it's a leaf node, return distance 1
        if (node.left == null && node.right == null) {
            int[] distances = new int[distance + 1];
            distances[1] = 1; // Leaf nodes are at distance 1
            return distances;
        }

        // Recursively get distances for left and right subtrees
        int[] leftDistances = dfs(node.left, distance, result);
        int[] rightDistances = dfs(node.right, distance, result);

        // Count valid pairs between left and right distances
        for (int i = 1; i <= distance; i++) {
            for (int j = 1; j <= distance; j++) {
                if (i + j <= distance) {
                    result[0] += leftDistances[i] * rightDistances[j];
                }
            }
        }

        // Update distances for the current node
        int[] currentDistances = new int[distance + 1];
        for (int i = 1; i < distance; i++) {
            currentDistances[i + 1] = leftDistances[i] + rightDistances[i];
        }

        return currentDistances;
    }
}
```

### Accepted
![Screenshot 2025-01-19 at 3 36 35 PM](https://github.com/user-attachments/assets/2cc2498c-883c-4f7d-b02c-4c51e8901b9b)
