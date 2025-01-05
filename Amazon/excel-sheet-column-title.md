# Excel Sheet Column Title

[Problem Link](https://leetcode.com/problems/excel-sheet-column-title/description/) 

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet. The columns are labeled with 
letters starting from "A" for 1, "B" for 2, ..., "Z" for 26, "AA" for 27, and so on. Your task is to convert the given column number 
into its respective Excel column title.

### Sample Input 1
```
columnNumber = 1
```
### Sample Output 1
```
"A"
```

### Sample Input 2
```
columnNumber = 28
```
### Sample Output 2
```
"AB"
```

### Solution
```java
class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder result = new StringBuilder();
        
        // Loop until columnNumber becomes zero
        while (columnNumber > 0) {
            // Subtract 1 to handle 1-indexed system
            columnNumber--;
            
            // Find the remainder when divided by 26
            char currentChar = (char) (columnNumber % 26 + 'A');
            
            // Append the character to the result
            result.insert(0, currentChar);
            
            // Update columnNumber for the next iteration
            columnNumber /= 26;
        }
        
        return result.toString();
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 9 41 33 PM](https://github.com/user-attachments/assets/de8860db-bb60-41e9-96b0-412120b7f39a)
