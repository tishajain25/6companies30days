# Minimum Non-Zero Product of the Array Elements

[Problem Link](https://leetcode.com/problems/minimum-non-zero-product-of-the-array-elements/description/) 

Given a positive integer p, construct an array nums containing all integers from 1 to 2^p - 1. You can perform the following operation any number of times:

. Pick two numbers x and y from nums.
. Swap any bit in x with the corresponding bit in y.

Your task is to find the minimum non-zero product of all elements in nums after performing the operations. Return the result modulo 10^9 + 7.

### Sample Input 1
```
p=1
```
### Sample Output 1
```
1
```

### Sample Input 2
```
p=2
```
### Sample Output 2
```
6
```

### Solution
```java
class Solution {
    public int minNonZeroProduct(int p) {
        final int mod = (int) 1e9 + 7;
        long a = ((1L << p) - 1) % mod;
        long b = qpow(((1L << p) - 2) % mod, (1L << (p - 1)) - 1, mod);
        return (int) (a * b % mod);
    }

    private long qpow(long a, long n, int mod) {
        long ans = 1;
        for (; n > 0; n >>= 1) {
            if ((n & 1) == 1) {
                ans = ans * a % mod;
            }
            a = a * a % mod;
        }
        return ans;
    }
}
```

### Accepted
![Screenshot 2025-01-22 at 12 31 00 PM](https://github.com/user-attachments/assets/1eac65a7-3047-42e1-a53f-1da959f51b4c)
