# Maximum Sum BST in Binary Tree

[Problem Link](https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/description/)

Given a binary tree, find the maximum sum of all keys of any sub-tree that is also a Binary Search Tree (BST). A Binary Search Tree is defined as a tree where the left subtree of a node contains only nodes with keys less than the node’s key, and the right subtree contains only nodes with keys greater than the node’s key. The left and right subtrees must also be BSTs.

Return the maximum sum of all BSTs in the tree.

### Sample Input 1
```
root = [1,4,3,2,4,2,5,null,null,null,null,null,null,4,6]
```

### Sample Output 1
```
20
```

### Sample Input 2
```
root = [4,3,null,1,2]
```

### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    private int ans;
    private final int inf = 1 << 30;

    public int maxSumBST(TreeNode root) {
        dfs(root);
        return ans;
    }

    private int[] dfs(TreeNode root) {
        if (root == null) {
            return new int[] {1, inf, -inf, 0};
        }
        var l = dfs(root.left);
        var r = dfs(root.right);
        int v = root.val;
        if (l[0] == 1 && r[0] == 1 && l[2] < v && r[1] > v) {
            int s = v + l[3] + r[3];
            ans = Math.max(ans, s);
            return new int[] {1, Math.min(l[1], v), Math.max(r[2], v), s};
        }
        return new int[4];
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 25 30 PM](https://github.com/user-attachments/assets/5fb91c65-3d1e-4a33-b751-823cce362b00)
