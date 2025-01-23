# Query Kth Smallest Trimmed Number

[Problem Link](https://leetcode.com/problems/query-kth-smallest-trimmed-number/description/) 

You are given an array of strings nums, where each string is of equal length and consists of only digits. You are also given a 2D array queries, where each query consists of two integers [k, trim]. For each query, you need to:

Trim each number in nums to its rightmost trim digits.
Find the index of the k-th smallest trimmed number in nums. If two numbers are equal after trimming, the one with the smaller index is considered smaller.
Return an array of answers where each element is the result of the corresponding query.

### Sample Input 
```
nums = ["102","473","251","814"]
queries = [[1,1],[2,3],[4,2],[1,2]]
```
### Sample Output 
```
[2, 2, 1, 0]
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
![Screenshot 2025-01-16 at 9 23 45 PM](https://github.com/user-attachments/assets/67483b5d-b249-478f-94dd-39dab2504be5)
