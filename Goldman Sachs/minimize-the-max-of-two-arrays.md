# Minimize the Maximum of Two Arrays

[Problem Link](https://leetcode.com/problems/minimize-the-maximum-of-two-arrays/description/) 

You are given two integers divisor1 and divisor2 and two counts uniqueCnt1 and uniqueCnt2. You need to create two arrays:

1. arr1 with uniqueCnt1 distinct integers, none of which are divisible by divisor1.
2. arr2 with uniqueCnt2 distinct integers, none of which are divisible by divisor2.

Additionally:
. No integer should appear in both arrays.

Find the minimum possible maximum integer that can appear in either array.

### Sample Input 
```
divisor1 = 2, divisor2 = 7, uniqueCnt1 = 1, uniqueCnt2 = 3
```
### Sample Output 
```
4
```

### Solution
```java
class Solution {
    public int minimizeSet(int divisor1, int divisor2, int uniqueCnt1, int uniqueCnt2) {
       final long divisorLcm = lcm(divisor1, divisor2);
    long l = 0;
    long r = Integer.MAX_VALUE;

    while (l < r) {
        final long m = (l + r) / 2;
        if (isPossible(m, divisorLcm, divisor1, divisor2, uniqueCnt1, uniqueCnt2))
            r = m;
        else
            l = m + 1;
        }

        return (int) l;
    }

  // Returns true if we can take uniqueCnt1 integers from [1..m] to arr1 and
  // take uniqueCnt2 integers from [1..m] to arr2.
    private boolean isPossible(long m, long divisorLcm, int divisor1, int divisor2, int uniqueCnt1,
                             int uniqueCnt2) {
        final long cnt1 = m - m / divisor1;
        final long cnt2 = m - m / divisor2;
        final long totalCnt = m - m / divisorLcm;
        return cnt1 >= uniqueCnt1 && cnt2 >= uniqueCnt2 && totalCnt >= uniqueCnt1 + uniqueCnt2;
    }

    private long gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }

    private long lcm(int a, int b) {
        return a * (b / gcd(a, b));
    }
}
```

### Accepted
![Screenshot 2025-01-23 at 1 52 51 PM](https://github.com/user-attachments/assets/da22104a-b16c-41f7-b7d7-a300645ec282)
