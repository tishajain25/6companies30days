# Number following a pattern

[Problem Link](https://www.geeksforgeeks.org/problems/number-following-a-pattern3126/1) 


Given a string pattern containing only 'I' (for increasing) and 'D' (for decreasing), return the smallest number that follows the pattern. The number must be formed using digits from 1 to 9 without repetition.

. 'I' means the next digit should be greater.
. 'D' means the next digit should be smaller.

### Sample Input 1
```
"D"
```

### Sample Output 1
```
"21"
```

### Sample Input 2
```
"IIDDD"
```

### Sample Output 2
```
"126543"
```

### Solution
```java
class Solution{
    static String printMinNumberForPattern(String S){
        // code here
        int n = S.length();
        Stack<Integer> stack = new Stack<>();
        StringBuilder result = new StringBuilder();

        // We go through the pattern and also push numbers into the stack.
        for (int i = 0; i <= n; i++) {
            // Push the current number (i+1)
            stack.push(i + 1);

            // If we reach the end of the pattern or the current pattern is 'I'
            // we pop the stack and append to result
            if (i == n || S.charAt(i) == 'I') {
                while (!stack.isEmpty()) {
                    result.append(stack.pop());
                }
            }
        }

        return result.toString();
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.printMinNumberForPattern("D"));      // Output: "21"
        System.out.println(sol.printMinNumberForPattern("IIDDD"));  // Output: "126543"
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 10 52 PM](https://github.com/user-attachments/assets/2f4321e5-e530-4191-a43b-7826c06d11a8)
