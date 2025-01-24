# Combination Sum III

[Problem Link](https://leetcode.com/problems/combination-sum-iii/description/) 


You are given two integers k and n. You need to find all unique combinations of k distinct numbers from the range 1 to 9 that sum up 
to n. Each number can be used only once in the combination.

Return a list of all valid combinations.

### Sample Input 
```
k = 3, n = 7
```

### Sample Output 
```
[[1, 2, 4]]
```

### Solution
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(k, n, 1, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int k, int n, int start, List<Integer> current, List<List<Integer>> result) {
        // If the combination has k elements and the sum equals n, add it to the result
        if (current.size() == k && n == 0) {
            result.add(new ArrayList<>(current));
            return;
        }

        // If the combination exceeds k elements or the sum exceeds n, stop exploring further
        if (current.size() > k || n < 0) {
            return;
        }

        // Try adding each number from start to 9 to the current combination
        for (int i = start; i <= 9; i++) {
            current.add(i); // Add the current number
            backtrack(k, n - i, i + 1, current, result); // Recursively try next numbers
            current.remove(current.size() - 1); // Backtrack, remove the last number
        }
    }
}
```

### Accepted
![Screenshot 2025-01-24 at 3 52 12 PM](https://github.com/user-attachments/assets/d1e485af-1122-4a7f-8a53-e2347e1d973b)
