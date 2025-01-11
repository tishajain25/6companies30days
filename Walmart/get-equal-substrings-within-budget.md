# Get Equal Substrings Within Budget

[Problem Link](https://leetcode.com/problems/get-equal-substrings-within-budget/description/) 

Given two strings s and t of the same length, and an integer maxCost, find the maximum length of a substring of s that can be changed to match the corresponding 
substring of t with a total cost less than or equal to maxCost. The cost of changing a character is the absolute difference of their ASCII values.

### Sample Input 1
```
s = "abcd", t = "bcdf", maxCost = 3
```
### Sample Output 1
```
3
```

### Sample Input 2
```
s = "abcd", t = "cdef", maxCost = 3
```
### Sample Output 2
```
1
```

### Solution
```java
class Solution {
    public int equalSubstring(String s, String t, int maxCost) {
        int n = s.length();
        int left = 0, right = 0, currentCost = 0, maxLength = 0;

        while (right < n) {
            // Calculate the cost of changing the current character
            currentCost += Math.abs(s.charAt(right) - t.charAt(right));

            // If the cost exceeds maxCost, shrink the window from the left
            while (currentCost > maxCost) {
                currentCost -= Math.abs(s.charAt(left) - t.charAt(left));
                left++;
            }

            // Update the maximum length of the valid window
            maxLength = Math.max(maxLength, right - left + 1);
            right++;
        }

        return maxLength;
    }
}
```

### Accepted
![Screenshot 2025-01-11 at 10 01 56 PM](https://github.com/user-attachments/assets/a030ed25-7300-430b-9bb9-6861063b7826)

