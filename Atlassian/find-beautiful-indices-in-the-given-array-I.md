# Find Beautiful Indices in the Given Array I

[Problem Link](https://leetcode.com/problems/find-beautiful-indices-in-the-given-array-i/description/) 

Given a string s, two substrings a and b, and an integer k, find all indices i in s such that:

The substring s[i..i + a.length - 1] matches a.
There exists an index j such that s[j..j + b.length - 1] matches b and ∣j−i∣≤k.

Return these indices in sorted order.

### Sample Input 
```
s = "isawsquirrelnearmysquirrelhouseohmy", a = "my", b = "squirrel", k = 15
```
### Sample Output 
```
[16, 33]
```


### Solution
```java
class Solution {
    public List<Integer> beautifulIndices(String s, String a, String b, int k) {
        List<Integer> aIndices = new ArrayList<>();
        List<Integer> bIndices = new ArrayList<>();
        List<Integer> result = new ArrayList<>();

        // Find all indices where `a` and `b` occur
        for (int i = 0; i <= s.length() - a.length(); i++) {
            if (s.substring(i, i + a.length()).equals(a)) {
                aIndices.add(i);
            }
        }

        for (int j = 0; j <= s.length() - b.length(); j++) {
            if (s.substring(j, j + b.length()).equals(b)) {
                bIndices.add(j);
            }
        }

        // Use two pointers to find valid indices
        int j = 0;
        for (int i : aIndices) {
            while (j < bIndices.size() && bIndices.get(j) < i - k) {
                j++;
            }
            if (j < bIndices.size() && Math.abs(bIndices.get(j) - i) <= k) {
                result.add(i);
            }
        }

        return result;
    }
}
```

### Accepted
![Screenshot 2025-01-22 at 11 56 39 AM](https://github.com/user-attachments/assets/69f1416b-c3ed-4277-b953-a30912e4ac1e)
