# Construct the Longest New String

[Problem Link](https://leetcode.com/problems/construct-the-longest-new-string/description/) 

You are given three integers x, y, and z, representing the number of strings "AA", "BB", and "AB", respectively. Your task is to concatenate these 
strings to form the longest  possible string such that it does not contain "AAA" or "BBB" as substrings. Return the maximum length of such a string.

Return the distance value between the two arrays.

### Sample Input 1
```
x=2,y=5,z=1
```
### Sample Output 1
```
12
```

### Sample Input 2
```
x=3,y=2,z=2
```
### Sample Output 2
```
14
```

### Solution
```java
class Solution {
    public int longestString(int x, int y, int z) {
     // Minimum alternations possible between "AA" and "BB"
        int minAlternations = Math.min(x, y);

        // Total length contributed by alternations
        int alternatingLength = minAlternations * 4;

        // Add "AB" strings freely (2 characters each)
        int abLength = z * 2;

        // Add one extra "AA" or "BB" if possible
        int remainingAAorBB = (x > y ? x - minAlternations : y - minAlternations) > 0 ? 2 : 0;

        // Total maximum length
        return alternatingLength + abLength + remainingAAorBB;
    }
}
```

### Accepted
![Screenshot 2025-01-23 at 12 22 03 PM](https://github.com/user-attachments/assets/888d7151-89c4-402f-8c58-436bd7b1993e)
