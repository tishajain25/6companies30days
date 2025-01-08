# Nuts and Bolts Problem

[Problem Link](https://www.geeksforgeeks.org/problems/nuts-and-bolts-problem0431/1) 

Given two arrays nuts[] and bolts[] of size n, where each nut corresponds to a bolt, match the nuts and bolts by sorting both 
arrays in lexicographical order based on the predefined order: {!, #, $, %, &, *, ?, @, ^}. You can only compare a nut with a 
bolt, not two nuts or two bolts.


### Sample Input 1
```
n = 5
nuts[] = {'@', '%', '$', '#', '^'}
bolts[] = {'%', '@', '#', '$', '^'}
```
### Sample Output 1
```
nuts[] = {'#', '$', '%', '@', '^'}
bolts[] = {'#', '$', '%', '@', '^'}
```

### Sample Input 2
```
n = 9
nuts[] = {'^', '&', '%', '@', '#', '*', '$', '?', '!'}
bolts[] = {'?', '#', '@', '%', '&', '*', '$', '^', '!'}  
```
### Sample Output 2
```
nuts[] = {'!', '#', '$', '%', '&', '*', '?', '@', '^'}
bolts[] = {'!', '#', '$', '%', '&', '*', '?', '@', '^'}
```

### Solution
```java
class Solution {
    void matchPairs(int n, char nuts[], char bolts[]) {
        // code here
        // Define the order of precedence
        char[] order = {'!', '#', '$', '%', '&', '*', '?', '@', '^'};

        // Create a hash set for nuts
        Set<Character> nutSet = new HashSet<>();
        for (char nut : nuts) {
            nutSet.add(nut);
        }

        // Sort the nuts and bolts according to the predefined order
        int index = 0;
        for (char c : order) {
            if (nutSet.contains(c)) {
                nuts[index] = c;
                bolts[index] = c;
                index++;
            }
        }
    }
}
```

### Accepted
![Screenshot 2025-01-08 at 9 14 29 AM](https://github.com/user-attachments/assets/e1f51f58-1d2d-452c-9b0a-14a2232596da)
