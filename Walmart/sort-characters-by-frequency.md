# Sort Characters By Frequency

[Problem Link](https://leetcode.com/problems/sort-characters-by-frequency/description/) 

Given a string s, rearrange its characters in decreasing order of their frequency. If multiple arrangements are possible, return any valid one.


### Sample Input 1
```
s = "tree"
```
### Sample Output 1
```
"eert" or "eetr"
```

### Sample Input 2
```
s = "cccaaa"
```
### Sample Output 2
```
"aaaccc" or "cccaaa"
```

### Solution
```java
class Solution {
    public String frequencySort(String s) {
        // Step 1: Count frequencies of each character
        Map<Character, Integer> frequencyMap = new HashMap<>();
        for (char c : s.toCharArray()) {
            frequencyMap.put(c, frequencyMap.getOrDefault(c, 0) + 1);
        }

        // Step 2: Sort characters by frequency
        List<Character> characters = new ArrayList<>(frequencyMap.keySet());
        characters.sort((a, b) -> frequencyMap.get(b) - frequencyMap.get(a));

        // Step 3: Build the result string
        StringBuilder result = new StringBuilder();
        for (char c : characters) {
            int freq = frequencyMap.get(c);
            for (int i = 0; i < freq; i++) {
                result.append(c);
            }
        }

        return result.toString();
    }
}
```

### Accepted
![Screenshot 2025-01-15 at 8 19 46 PM](https://github.com/user-attachments/assets/4e7ffcbe-e050-402e-8da4-0d41ba28400c)
