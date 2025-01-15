# Destroying Asteroids

[Problem Link](https://leetcode.com/problems/destroying-asteroids/description/) 

Given a planet with an initial mass and an array of asteroid masses, determine if the planet can destroy all asteroids. The planet can destroy an asteroid if its mass is 
greater than or equal to the asteroid's mass, absorbing the asteroid's mass after destruction. Return true if all asteroids can be destroyed; otherwise, return false.

### Sample Input 1
```
mass = 10, asteroids = [3, 9, 19, 5, 21]
```
### Sample Output 1
```
true
```

### Sample Input 2
```
mass = 5, asteroids = [4, 9, 23, 4]
```
### Sample Output 2
```
false
```

### Solution
```java
class Solution {
    public boolean asteroidsDestroyed(int mass, int[] asteroids) {
       // Sort the asteroids in ascending order
        Arrays.sort(asteroids);
        
        long currentMass = mass; // Use long to prevent overflow
        for (int asteroid : asteroids) {
            if (currentMass >= asteroid) {
                currentMass += asteroid; // Absorb the asteroid's mass
            } else {
                return false; // Planet cannot destroy this asteroid
            }
        }
        return true; // All asteroids destroyed
    }
}
```

### Accepted
![Screenshot 2025-01-15 at 8 47 36 PM](https://github.com/user-attachments/assets/cabbd2a1-aa47-475d-be47-012596ed9893)
