# Extra Characters in a String

[Problem Link](https://leetcode.com/problems/extra-characters-in-a-string/description/) 

Given a string s and a list of words dictionary, split s into substrings where each substring is a word from dictionary. Minimize 
the number of extra characters in s that cannot be used in any valid substring.

### Sample Input 1
```
s = "leetscode"
dictionary = ["leet", "code", "leetcode"]
```
### Sample Output 1
```
1
```

### Sample Input 2
```
s = "sayhelloworld"
dictionary = ["hello", "world"]
```
### Sample Output 2
```
3
```

### Solution
```java
class Solution {
    public int minExtraChar(String s, String[] dictionary) {
        // Convert dictionary into a HashSet for quick lookup
        Set<String> wordSet = new HashSet<>(Arrays.asList(dictionary));
        
        int n = s.length();
        int[] dp = new int[n + 1];
        
        // Initialize DP array with maximum possible value
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0; // No extra characters for an empty string
        
        // Iterate through each index of the string
        for (int i = 1; i <= n; i++) {
            dp[i] = dp[i - 1] + 1; // Assume current character is extra
            
            // Check all possible substrings ending at i
            for (int j = i; j > 0; j--) {
                String substring = s.substring(j - 1, i);
                if (wordSet.contains(substring)) {
                    dp[i] = Math.min(dp[i], dp[j - 1]);
                }
            }
        }
        
        return dp[n];
    }
}
```

### Accepted
![Screenshot 2025-01-15 at 8 29 13 PM](https://github.com/user-attachments/assets/7e8e36fb-3374-442c-90e1-617752767d08)
