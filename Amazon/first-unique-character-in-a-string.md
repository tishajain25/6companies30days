# First Unique Character in a String

[Problem Link](https://leetcode.com/problems/first-unique-character-in-a-string/description/) 

Given a string s, find the index of the first non-repeating character. If no such character exists, return -1.

### Sample Input 1
```
s = "leetcode"
```
### Sample Output 1
```
0
```

### Sample Input 2
```
s = "loveleetcode"
```
### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    public int firstUniqChar(String s) {
        // Step 1: Create a HashMap to store the frequency of each character
        HashMap<Character, Integer> frequencyMap = new HashMap<>();
        
        // Step 2: Populate the frequency map
        for (char c : s.toCharArray()) {
            frequencyMap.put(c, frequencyMap.getOrDefault(c, 0) + 1);
        }
        
        // Step 3: Traverse the string to find the first unique character
        for (int i = 0; i < s.length(); i++) {
            if (frequencyMap.get(s.charAt(i)) == 1) {
                return i;  // Return the index of the first unique character
            }
        }
        
        // If no unique character is found, return -1
        return -1;
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 9 20 59 PM](https://github.com/user-attachments/assets/82e40a20-ebb6-4901-8699-e0e99157694c)
