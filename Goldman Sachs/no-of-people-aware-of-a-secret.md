# Number of People Aware of a Secret

[Problem Link](https://leetcode.com/problems/number-of-people-aware-of-a-secret/description/) 


You are given n days, a delay, and a forget period:

. On Day 1, one person learns a secret.
. A person starts sharing the secret after delay days.
. A person forgets the secret after forget days and stops sharing.
Find the total number of people who know the secret at the end of n days, modulo 10^9 + 7.

### Sample Input 
```
n = 6, delay = 2, forget = 4
```

### Sample Output 
```
5
```

### Solution
```java
class Solution {
    private static final int MOD = (int) 1e9 + 7;

    public int peopleAwareOfSecret(int n, int delay, int forget) {
        int m = (n << 1) + 10;
        long[] d = new long[m];
        long[] cnt = new long[m];
        cnt[1] = 1;
        for (int i = 1; i <= n; ++i) {
            if (cnt[i] > 0) {
                d[i] = (d[i] + cnt[i]) % MOD;
                d[i + forget] = (d[i + forget] - cnt[i] + MOD) % MOD;
                int nxt = i + delay;
                while (nxt < i + forget) {
                    cnt[nxt] = (cnt[nxt] + cnt[i]) % MOD;
                    ++nxt;
                }
            }
        }
        long ans = 0;
        for (int i = 1; i <= n; ++i) {
            ans = (ans + d[i]) % MOD;
        }
        return (int) ans;
    }
}
```

### Accepted
![Screenshot 2025-01-28 at 8 58 43 PM](https://github.com/user-attachments/assets/e3254049-03b2-4ef2-8f5d-8010d93d7bf5)
