# Count Words Obtained After Adding a Letter

[Problem Link](https://leetcode.com/problems/count-words-obtained-after-adding-a-letter/description/) 

You are given two arrays of strings, startWords and targetWords. For each word in targetWords, determine if it can be formed by:

1. Adding exactly one new letter to a word in startWords.
2. Rearranging the letters of the modified word.

Return the count of such words in targetWords.

### Sample Input 1
```
startWords = ["ant", "act", "tack"]
targetWords = ["tack", "act", "acti"]
```
### Sample Output 1
```
2
```

### Sample Input 2
```
startWords = ["ab", "a"]
targetWords = ["abc", "abcd"]
```
### Sample Output 2
```
1
```

### Solution
```java
class Solution {
    public int wordCount(String[] startWords, String[] targetWords) {
      Set<Integer> startWordMasks = new HashSet<>();
        
        // Convert each start word into a bitmask and store in a set
        for (String word : startWords) {
            startWordMasks.add(toBitmask(word));
        }
        
        int count = 0;
        
        // For each target word, check if it can be formed
        for (String target : targetWords) {
            int targetMask = toBitmask(target);
            
            // Remove one letter at a time and check if the resulting mask exists in startWordMasks
            for (char c : target.toCharArray()) {
                int modifiedMask = targetMask ^ (1 << (c - 'a'));
                if (startWordMasks.contains(modifiedMask)) {
                    count++;
                    break;
                }
            }
        }
        
        return count;
    }
    
    // Helper function to convert a word into a bitmask
    private int toBitmask(String word) {
        int mask = 0;
        for (char c : word.toCharArray()) {
            mask |= 1 << (c - 'a');
        }
        return mask;
    }
}
```

### Accepted
![Screenshot 2025-01-22 at 12 26 21 PM](https://github.com/user-attachments/assets/8058f9ee-3e45-45f3-bc19-472feed55ebc)
