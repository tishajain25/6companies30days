# Word Break

[Problem Link](https://leetcode.com/problems/word-break/) 

Given a string s and a list of words wordDict, determine if s can be segmented into one or more words from wordDict. Words in wordDict can be reused.

### Sample Input 1
```
s = "leetcode"
wordDict = ["leet", "code"]
```
### Sample Output 1
```
true
```

### Sample Input 2
```
s = "applepenapple"
wordDict = ["apple", "pen"]
```
### Sample Output 2
```
true
```

### Solution
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<>(wordDict); // Convert wordDict to a set for O(1) lookup
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true; // Empty string can be segmented

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.length()];
    }
}
```

### Accepted
![Screenshot 2025-01-15 at 8 23 47 PM](https://github.com/user-attachments/assets/34317e52-4809-47f6-a49f-23f0cc44a149)
