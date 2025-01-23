# Problem
<a href="https://leetcode.com/problems/number-of-people-aware-of-a-secret/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

On day 1, one person discovers a secret.

You are given an integer delay, which means that each person will share the secret with a new person every day, starting from delay days after discovering the secret. You are also given an integer forget, which means that each person will forget the secret forget days after discovering it. A person cannot share the secret on the same day they forgot it, or on any day afterwards.

Given an integer n, return the number of people who know the secret at the end of day n. Since the answer may be very large, return it modulo 109 + 7.

...

### Sample Input
```
n = 6, delay = 2, forget = 4
```
### Sample Output
```
5
```

### Solution
```cpp
class Solution {
public:
    int peopleAwareOfSecret(int n, int delay, int forget) {
        vector<long long> dp(forget, 0);
        dp[0] = 1;
        long long mod = 1e9 + 7;

        for (int i = 1; i < n; ++i) {
            dp[i % forget] = (mod + dp[(i + forget - delay) % forget] - dp[i % forget] + (i == 1 ? 0 : dp[(i - 1) % forget])) % mod;
        }

        long long ans = 0;
        for (int i = 0; i < forget; ++i) {
            ans = (ans + dp[i]) % mod;
        }
        return ans;
    }
};
```
