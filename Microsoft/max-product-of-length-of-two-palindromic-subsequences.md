# Maximum Product of the Length of Two Palindromic Subsequences

[Problem Link](https://leetcode.com/problems/maximum-product-of-the-length-of-two-palindromic-subsequences/description/) 

Given a string s, find two disjoint palindromic subsequences such that the product of their lengths is maximized. A subsequence is derived by deleting 
some or no characters without changing the order of the remaining characters. Two subsequences are disjoint if they do not pick a character at the same index.

Return the maximum product of the lengths of the two subsequences. If no valid subsequences exist, return 0.

### Sample Input 1
```
s = "leetcodecom"
```
### Sample Output 1
```
9
```

### Sample Input 2
```
s = "bb"
```
### Sample Output 2
```
1
```

### Solution
```java
class Solution {
    public int maxProduct(String s) {
        int n = s.length();
        int maxProduct = 0;

        // Step 1: Precompute all palindromic subsequences using bitmasking
        List<Integer> palindromes = new ArrayList<>();
        Map<Integer, Integer> lengthMap = new HashMap<>();

        for (int mask = 1; mask < (1 << n); mask++) {
            if (isPalindrome(s, mask)) {
                palindromes.add(mask);
                lengthMap.put(mask, Integer.bitCount(mask));
            }
        }

        // Step 2: Check all pairs of palindromic subsequences
        for (int i = 0; i < palindromes.size(); i++) {
            for (int j = i + 1; j < palindromes.size(); j++) {
                int mask1 = palindromes.get(i);
                int mask2 = palindromes.get(j);

                // Ensure the two subsequences are disjoint
                if ((mask1 & mask2) == 0) {
                    int len1 = lengthMap.get(mask1);
                    int len2 = lengthMap.get(mask2);
                    maxProduct = Math.max(maxProduct, len1 * len2);
                }
            }
        }

        return maxProduct;
    }

    // Helper function to check if a subsequence is a palindrome
    private boolean isPalindrome(String s, int mask) {
        StringBuilder subseq = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if ((mask & (1 << i)) != 0) {
                subseq.append(s.charAt(i));
            }
        }
        String str = subseq.toString();
        return str.equals(subseq.reverse().toString());
    }
}
```

### Accepted
![Screenshot 2025-01-05 at 8 41 53 PM](https://github.com/user-attachments/assets/21074b10-9724-4d38-bd46-13cf0d8c0008)
