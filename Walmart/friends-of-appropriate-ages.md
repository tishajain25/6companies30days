# Friends Of Appropriate Ages

[Problem Link](https://leetcode.com/problems/friends-of-appropriate-ages/description/) 

Given an array ages where ages[i] represents the age of the i-th person, calculate the total number of friend requests sent based on 
the following rules:

A Person x will not send a friend request to a person y (x != y) if any of the following conditions is true:

age[y] <= 0.5 * age[x] + 7
age[y] > age[x]
age[y] > 100 && age[x] < 100

Otherwise, x will send a friend request to y.

A person cannot send a friend request to themselves.


### Sample Input 1
```
ages = [16, 16]
```
### Sample Output 1
```
2
```

### Sample Input 2
```
ages = [16, 17, 18]
```
### Sample Output 2
```
2
```

### Solution
```java
class Solution {
    public int numFriendRequests(int[] ages) {
        int[] count = new int[121]; // Frequency array for ages
        
        // Count the occurrences of each age
        for (int age : ages) {
            count[age]++;
        }

        int totalRequests = 0;

        // Iterate over all possible age pairs
        for (int ageX = 1; ageX <= 120; ageX++) {
            for (int ageY = 1; ageY <= 120; ageY++) {
                if (count[ageX] == 0 || count[ageY] == 0) continue;

                // Check if ageX can send a friend request to ageY
                if (ageY > 0.5 * ageX + 7 && ageY <= ageX) {
                    if (ageX == ageY) {
                        // If both ages are the same, each person can send requests to the others
                        totalRequests += count[ageX] * (count[ageX] - 1);
                    } else {
                        // Different ages
                        totalRequests += count[ageX] * count[ageY];
                    }
                }
            }
        }

        return totalRequests;
    }
}
```

### Accepted
![Screenshot 2025-01-12 at 12 27 02 PM](https://github.com/user-attachments/assets/b5149657-4cb2-478f-9561-02e38d7f1cc2)
