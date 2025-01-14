# Verify Preorder Serialization of a Binary Tree

[Problem Link](https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/description/) 

Check if a given preorder string of a binary tree, using integers and # for nulls, is a valid serialization based on binary tree rules.

### Sample Input 1
```
preorder = "9,3,4,#,#,1,#,#,2,#,6,#,#"
```
### Sample Output 1
```
true
```

### Sample Input 2
```
preorder = "1,#"
```
### Sample Output 2
```
false
```

### Solution
```java
class Solution {
    public boolean isValidSerialization(String preorder) {
        // Split the string into nodes
        String[] nodes = preorder.split(",");
        int slots = 1; // Start with one slot for the root
        
        for (String node : nodes) {
            // Consume one slot for the current node
            slots--;
            // If slots are negative, the serialization is invalid
            if (slots < 0) return false;
            // If the node is not null, add two slots for its children
            if (!node.equals("#")) {
                slots += 2;
            }
        }
        // All slots should be used up
        return slots == 0;
    }
}
```

### Accepted
![Screenshot 2025-01-14 at 8 13 30 AM](https://github.com/user-attachments/assets/47f86a90-1d24-40b6-9a5d-ce262a83b243)
