# Problem
<a href="https://leetcode.com/problems/count-the-number-of-square-free-subsets/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a positive integer 0-indexed array nums.

A subset of the array nums is square-free if the product of its elements is a square-free integer.

A square-free integer is an integer that is divisible by no square number other than 1.

Return the number of square-free non-empty subsets of the array nums. Since the answer may be too large, return it modulo 109 + 7.

A non-empty subset of nums is an array that can be obtained by deleting some (possibly none but not all) elements from nums. Two subsets are different if and only if the chosen indices to delete are different.

### Sample Input
```
nums = [3,4,4,5]
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
public:
    vector<int> primes;
    long long int mod;

    long long int countSubsets(int idx, long long int maskUsed, vector<int>& nums) {
        
        auto getPrimeMask = [&](long long int num) -> long long int {
            long long int mask = 0;
            for (int i = 0; i < 10; i++) {
                int count = 0;
                while (num % primes[i] == 0) {
                    count++;
                    num /= primes[i];
                }
                if (count > 1) {
                    return -1; 
                }
                if (count == 1) {
                    mask |= (1 << (i + 1));
                }
            }
            return mask;
        };

        if (idx >= nums.size()) return 1;
        if (dp[idx][maskUsed] != -1) return dp[idx][maskUsed];

        long long int mask = getPrimeMask(nums[idx]);
        long long int result = countSubsets(idx + 1, maskUsed, nums);

        if ((maskUsed & mask) == 0) {
            result = (result + countSubsets(idx + 1, maskUsed | mask, nums)) % mod;
        }

        return dp[idx][maskUsed] = result;
    }

    int squareFreeSubsets(vector<int>& nums) {
        mod = 1e9 + 7;
        memset(dp, -1, sizeof(dp));
        primes = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29};

        return (countSubsets(0, 1, nums) - 1 + mod) % mod; 
    }

private:
    long long int dp[1111][1 << 11];
};

```
