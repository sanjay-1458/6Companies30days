# Problem
<a href="https://leetcode.com/problems/destroying-asteroids/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer array nums. We call a subset of nums good if its product can be represented as a product of one or more distinct prime numbers.

For example, if nums = [1, 2, 3, 4]:
[2, 3], [1, 2, 3], and [1, 3] are good subsets with products 6 = 2*3, 6 = 2*3, and 3 = 3 respectively.
[1, 4] and [4] are not good subsets with products 4 = 2*2 and 4 = 2*2 respectively.
Return the number of different good subsets in nums modulo 109 + 7.

A subset of nums is any array that can be obtained by deleting some (possibly none or all) elements from nums. Two subsets are different if and only if the chosen indices to delete are different.

### Sample Input
```
nums = [1,2,3,4]
```
### Sample Output
```
6
```

### Solution
```cpp
class Solution {
public:
    int numberOfGoodSubsets(vector<int>& nums) {
        int mod = 1e9 + 7;
        int cnt = 10;
        vector<int> mask_(31, -1);
        vector<int> primes = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29};
        vector<int> count(31, 0);

        for (int &num : nums) {
            count[num]++;
        }

        for (int i = 1; i <= 30; ++i) {
            int mask = 0, num = i;
            bool isValid = true;
            for (int j = 0; j < cnt; ++j) {
                int prime = primes[j];
                if (num % prime == 0) {
                    if ((num / prime) % prime == 0) {
                        isValid = false;
                        break;
                    }
                    mask |= (1 << j);
                }
            }
            mask_[i] = isValid ? mask : -1;
        }

        vector<long long> dp(1 << cnt, 0);
        dp[0] = 1;

        for (int num = 1; num <= 30; ++num) {
            if (count[num] == 0 || mask_[num] == -1) continue;
            int mask = mask_[num];
            for (int j = (1 << cnt) - 1; j >= 0; --j) {
                if ((j & mask) == 0) {
                    dp[j | mask] = (dp[j | mask] + dp[j] * count[num]) % mod;
                }
            }
        }

        long long result = 0;
        for (int j = 1; j < (1 << cnt); ++j) {
            result = (result + dp[j]) % mod;
        }

        return result;
    }
};

```
