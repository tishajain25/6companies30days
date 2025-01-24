# Letter Combinations of a Phone Number

[Problem Link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/) 


Given a string of digits from 2 to 9, return all possible letter combinations that the number could represent based on a telephone keypad 
mapping. Each digit corresponds to a set of letters, and you need to generate all possible combinations of those letters.

### Sample Input 
```
"23"
```

### Sample Output 
```
["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

### Solution
```java
class Solution {
    private static final String[] phoneMap = {
        "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
    };

    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return result;
        }
        backtrack(digits, 0, new StringBuilder(), result);
        return result;
    }

    private void backtrack(String digits, int index, StringBuilder current, List<String> result) {
        if (index == digits.length()) {
            result.add(current.toString());
            return;
        }

        String letters = phoneMap[digits.charAt(index) - '0'];
        for (char letter : letters.toCharArray()) {
            current.append(letter);
            backtrack(digits, index + 1, current, result);
            current.deleteCharAt(current.length() - 1); // backtrack
        }
    }
}
```

### Accepted
![Screenshot 2025-01-24 at 4 19 58 PM](https://github.com/user-attachments/assets/aa0cf4e4-7555-473a-825f-87505a248028)
