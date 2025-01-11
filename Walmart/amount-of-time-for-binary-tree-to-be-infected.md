# Amount of Time for Binary Tree to Be Infected

[Problem Link](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/description/) 

Given the root of a binary tree and a starting node value, an infection spreads from the starting node to its adjacent nodes (parent and children) every minute. 
Return the total time (in minutes) required for the entire tree to be infected.


### Sample Input 1
```
root = [1,5,3,null,4,10,6,9,2], start = 3
```
### Sample Output 1
```
4
```

### Sample Input 2
```
root = [1], start = 1
```
### Sample Output 2
```
0
```

### Solution
```java
class Solution {
    public int amountOfTime(TreeNode root, int start) {
        // Step 1: Build graph representation of the tree
        Map<Integer, List<Integer>> graph = new HashMap<>();
        buildGraph(root, null, graph);

        // Step 2: Perform BFS to calculate infection time
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.add(start);
        visited.add(start);

        int time = 0;

        while (!queue.isEmpty()) {
            int size = queue.size();
            boolean spread = false;

            for (int i = 0; i < size; i++) {
                int node = queue.poll();
                for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                    if (!visited.contains(neighbor)) {
                        queue.add(neighbor);
                        visited.add(neighbor);
                        spread = true;
                    }
                }
            }

            if (spread) time++;
        }

        return time;
    }

    // Helper function to build the graph
    private void buildGraph(TreeNode node, TreeNode parent, Map<Integer, List<Integer>> graph) {
        if (node == null) return;

        graph.putIfAbsent(node.val, new ArrayList<>());
        if (parent != null) {
            graph.get(node.val).add(parent.val);
            graph.get(parent.val).add(node.val);
        }

        buildGraph(node.left, node, graph);
        buildGraph(node.right, node, graph);
    }
}
```

### Accepted
![Screenshot 2025-01-11 at 10 18 48 PM](https://github.com/user-attachments/assets/0f85e69b-e3cb-4f1f-bba3-5c66a08c00cc)

