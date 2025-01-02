# Bulls and Cows

[Problem Link](https://leetcode.com/problems/bulls-and-cows/description/) 

You are given a secret number and a friend's guess. Return a hint in the format "xAyB," where x is the number 
of bulls (correct digits in correct positions) and y is the number of cows (correct digits in incorrect positions).

### Sample Input 1
```
secret = "1807", guess = "7810"
```
### Sample Output 1
```
"1A3B"
```

### Sample Input 2
```
secret = "1123", guess = "0111"
```
### Sample Output 2
```
"1A1B"
```

### Solution
```java
class Solution {
    public String getHint(String secret, String guess) {
int bulls = 0;
        int cows = 0;
        int[] secretFreq = new int[10]; // To store frequency of digits in secret
        int[] guessFreq = new int[10]; // To store frequency of digits in guess

        // First pass: Count bulls and track unmatched digits
        for (int i = 0; i < secret.length(); i++) {
            if (secret.charAt(i) == guess.charAt(i)) {
                bulls++; // Matching digit and position
            } else {
                secretFreq[secret.charAt(i) - '0']++;
                guessFreq[guess.charAt(i) - '0']++;
            }
        }

        // Second pass: Count cows based on unmatched frequencies
        for (int i = 0; i < 10; i++) {
            cows += Math.min(secretFreq[i], guessFreq[i]);
        }

        // Format the result as "xAyB"
        return bulls + "A" + cows + "B";
    }
}
```

### Accepted
![Screenshot 2025-01-02 at 1 57 06 PM](https://github.com/user-attachments/assets/79560ddf-ca03-4730-946a-acb889ef42c6)
