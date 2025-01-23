# Count Collisions on a Road

[Problem Link](https://leetcode.com/problems/count-collisions-on-a-road/description/) 

You are given a string directions where each character represents a car's movement:

. 'L': Moves left.
. 'R': Moves right.
. 'S': Stays stationary.

When cars collide:
1. 'R' collides with 'L' → +2 collisions.
2. Moving cars ('R' or 'L') collide with 'S' → +1 collision.
After a collision, cars stop moving. Return the total number of collisions.

### Sample Input 
```
"RLRSLL"
```
### Sample Output 
```
5
```

### Solution
```java
class Solution {
    public int countCollisions(String directions) {
      int n = directions.length();
        int collisions = 0;
        boolean seenStationaryOrRight = false;

        // Count collisions for left-moving cars ('L')
        for (int i = 0; i < n; i++) {
            if (directions.charAt(i) == 'R') {
                seenStationaryOrRight = true;
            } else if (directions.charAt(i) == 'L' && seenStationaryOrRight) {
                collisions++;
            } else if (directions.charAt(i) == 'S') {
                seenStationaryOrRight = true;
            }
        }

        // Count collisions for right-moving cars ('R')
        seenStationaryOrRight = false;
        for (int i = n - 1; i >= 0; i--) {
            if (directions.charAt(i) == 'L') {
                seenStationaryOrRight = true;
            } else if (directions.charAt(i) == 'R' && seenStationaryOrRight) {
                collisions++;
            } else if (directions.charAt(i) == 'S') {
                seenStationaryOrRight = true;
            }
        }

        return collisions;
    }
}
```

### Accepted
![Screenshot 2025-01-23 at 11 52 04 AM](https://github.com/user-attachments/assets/4610b52e-9367-42a0-a668-30429fb97426)
