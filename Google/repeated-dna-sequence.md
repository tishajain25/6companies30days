# Repeated DNA Sequences

[Problem Link](https://leetcode.com/problems/repeated-dna-sequences/description/) 

You are given a string s representing a DNA sequence consisting of the characters 'A', 'C', 'G', and 'T'. 
Your task is to find all 10-letter-long substrings (sequences) that appear more than once in the string. 
You need to return these repeated sequences.



### Sample Input 
```
"AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
```
### Sample Output 
```
["AAAAACCCCC", "CCCCCAAAAA"]
```


### Solution
```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        Set<String> seen = new HashSet<>();  // Set to store substrings we have seen
        Set<String> result = new HashSet<>(); // Set to store repeated substrings
        
        // Loop through the string to extract all 10-letter substrings
        for (int i = 0; i <= s.length() - 10; i++) {
            String substring = s.substring(i, i + 10);  // Extract the 10-letter substring
            
            // Check if the substring is already in the 'seen' set
            if (seen.contains(substring)) {
                result.add(substring);  // If seen before, add to result set
            } else {
                seen.add(substring);  // Otherwise, add to seen set
            }
        }
        
        // Convert the result set to a list and return it
        return new ArrayList<>(result);
    }
}
```

### Accepted
![Screenshot 2025-01-02 at 9 51 25 PM](https://github.com/user-attachments/assets/486fe4de-e05d-44a2-ae25-61c1c90c65b0)
