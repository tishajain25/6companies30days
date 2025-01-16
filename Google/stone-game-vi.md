# Stone Game VI

[Problem Link](https://leetcode.com/problems/stone-game-vi/description/) 

Alice and Bob play a game with a pile of stones. Each stone has a value for Alice and Bob, given by aliceValues and bobValues. They take turns picking stones, starting with Alice, and aim to maximize their respective scores. Both players play optimally.
Determine the winner:

Return 1 if Alice wins.
Return -1 if Bob wins.
Return 0 if it's a draw.

### Sample Input 1
```
aliceValues = [1, 3], bobValues = [2, 1]
```
### Sample Output 1
```
1
```

### Sample Input 2
```
aliceValues = [1, 2], bobValues = [3, 1]
```
### Sample Output 2
```
0
```

### Solution
```java
class Solution {
    public int stoneGameVI(int[] aliceValues, int[] bobValues) {
        int n = aliceValues.length;
        int[][] stones = new int[n][2];
        
        // Combine values and store them with indices
        for (int i = 0; i < n; i++) {
            stones[i][0] = aliceValues[i] + bobValues[i]; // combined value
            stones[i][1] = i; // index
        }
        
        // Sort stones by combined value in descending order
        Arrays.sort(stones, (a, b) -> b[0] - a[0]);
        
        int aliceScore = 0, bobScore = 0;
        
        // Simulate the game
        for (int i = 0; i < n; i++) {
            int index = stones[i][1];
            if (i % 2 == 0) {
                // Alice's turn
                aliceScore += aliceValues[index];
            } else {
                // Bob's turn
                bobScore += bobValues[index];
            }
        }
        
        // Determine the result
        if (aliceScore > bobScore) {
            return 1;
        } else if (bobScore > aliceScore) {
            return -1;
        } else {
            return 0;
        }
    }
}
```

### Accepted
![Screenshot 2025-01-16 at 7 58 39 PM](https://github.com/user-attachments/assets/a83e5994-9837-47a6-aa4e-6fcfc6bfec94)
