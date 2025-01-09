# Serialize and Deserialize Binary Tree

[Problem Link](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/) 

Design an algorithm to serialize a binary tree into a string and deserialize the string back into the original binary tree structure. 
The solution should handle all possible tree structures, including empty trees.

### Sample Input 1
```
root = [1,2,3,null,null,4,5]  
```
### Sample Output 1
```
[1,2,3,null,null,4,5]
```

### Sample Input 2
```
root = []
```
### Sample Output 2
```
[]
```

### Solution
```java
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
       if (root == null) return "null";
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            TreeNode current = queue.poll();
            if (current == null) {
                sb.append("null,");
            } else {
                sb.append(current.val).append(",");
                queue.add(current.left);
                queue.add(current.right);
            }
        }
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.equals("null")) return null;
        String[] nodes = data.split(",");
        TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int i = 1;

        while (!queue.isEmpty()) {
            TreeNode current = queue.poll();
            if (!nodes[i].equals("null")) {
                current.left = new TreeNode(Integer.parseInt(nodes[i]));
                queue.add(current.left);
            }
            i++;
            if (!nodes[i].equals("null")) {
                current.right = new TreeNode(Integer.parseInt(nodes[i]));
                queue.add(current.right);
            }
            i++;
        }
        return root;
    }
}
```

### Accepted
![Screenshot 2025-01-09 at 1 41 44 PM](https://github.com/user-attachments/assets/d5695eb2-dc1f-4ac8-a89e-714a93ccaed6)
