# Count Subtrees With Max Distance Between Cities

[Problem Link](https://leetcode.com/problems/count-subtrees-with-max-distance-between-cities/description/) 

You are given a tree with n cities connected by n−1 edges. A subtree is a connected subset of cities. For each d (1 to n−1), 
find how many subtrees exist where the maximum distance between any two cities is exactly d. Return an array of size n−1, where the i-th element 
is the count of such subtrees for d=i+1.

### Sample Input 1
```
n = 4
edges = [[1,2],[2,3],[2,4]]
```
### Sample Output 1
```
[3, 4, 0]
```

### Sample Input 2
```
n = 2
edges = [[1,2]]
```
### Sample Output 2
```
[1]
```

### Solution
```java
class Solution {
    public int[] smallestTrimmedNumbers(String[] nums, int[][] queries) {
        int n = nums.length;
        int[] result = new int[queries.length];
        
        // Iterate through each query
        for (int i = 0; i < queries.length; i++) {
            int k = queries[i][0]; // k-th smallest
            int trim = queries[i][1]; // number of digits to trim
            
            // Create a list of pairs (index, trimmed number as string)
            List<Pair<Integer, String>> trimmedList = new ArrayList<>();
            for (int j = 0; j < n; j++) {
                String trimmedNum = nums[j].substring(nums[j].length() - trim);
                trimmedList.add(new Pair<>(j, trimmedNum)); // Store index and trimmed string
            }
            
            // Sort based on trimmed number lexicographically, if equal then by original index
            trimmedList.sort((a, b) -> {
                int compare = a.getValue().compareTo(b.getValue());
                if (compare == 0) {
                    return Integer.compare(a.getKey(), b.getKey());
                }
                return compare;
            });
            
            // Get the k-th smallest number's original index
            result[i] = trimmedList.get(k - 1).getKey(); // Get the index from the sorted list
        }
        
        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-17 at 1 22 50 PM](https://github.com/user-attachments/assets/f8be061b-8988-4b51-b412-047dc9bcf102)
