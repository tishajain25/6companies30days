# Throne Inheritance

[Problem Link](https://leetcode.com/problems/throne-inheritance/description/) 

Design a system to manage the inheritance order of a kingdom.

1. The king is the first in the inheritance order.
2. A birth adds a child to the parent's inheritance order.
3. A death excludes a person from the inheritance order, but their descendants remain valid successors.
4. You can query the current inheritance order, excluding the dead.

### Sample Input 
```
["ThroneInheritance", "birth", "birth", "birth", "birth", "birth", "birth", "getInheritanceOrder", "death", "getInheritanceOrder"]
[["king"], ["king", "andy"], ["king", "bob"], ["king", "catherine"], ["andy", "matthew"], ["bob", "alex"], ["bob", "asha"], [null], ["bob"], [null]]
```
### Sample Output 
```
[null, null, null, null, null, null, null, ["king", "andy", "matthew", "bob", "alex", "asha", "catherine"], null, ["king", "andy", "matthew", "alex", "asha", "catherine"]]
```

### Solution
```java
class ThroneInheritance {

    private String king; // The name of the king
    private Map<String, List<String>> familyTree; // Parent -> List of children
    private Set<String> dead; // Set of dead people

    public ThroneInheritance(String kingName) {
        this.king = kingName;
        this.familyTree = new HashMap<>();
        this.dead = new HashSet<>();
        this.familyTree.put(kingName, new ArrayList<>());
    }

    // Register a new child under a parent
    public void birth(String parentName, String childName) {
        familyTree.putIfAbsent(parentName, new ArrayList<>());
        familyTree.get(parentName).add(childName);
    }

    // Mark a person as dead
    public void death(String name) {
        dead.add(name);
    }

    // Get the current inheritance order
    public List<String> getInheritanceOrder() {
        List<String> order = new ArrayList<>();
        dfs(king, order);
        return order;
    }

    // Helper function for DFS traversal
    private void dfs(String current, List<String> order) {
        if (!dead.contains(current)) {
            order.add(current);
        }
        if (familyTree.containsKey(current)) {
            for (String child : familyTree.get(current)) {
                dfs(child, order);
            }
        }
    }
}
```

### Accepted
![Screenshot 2025-01-21 at 6 50 27 PM](https://github.com/user-attachments/assets/9a71bdd5-b28a-479d-9ff3-3e1db6148a7c)
