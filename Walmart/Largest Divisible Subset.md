# Problem
<a href="https://leetcode.com/problems/largest-divisible-subset/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:

answer[i] % answer[j] == 0, or
answer[j] % answer[i] == 0
If there are multiple solutions, return any of them.

### Sample Input
```
nums = [1,2,3]
```
### Sample Output
```
[1,2]
```

### Solution
```cpp
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        if (nums.size() == 1)
            return {nums[0]};
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<int> dp(n, 1), temp(n, -1);
        int len = 0, idx = -1;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] % nums[j] == 0 && dp[i] < dp[j] + 1) {
                    dp[i] = dp[j] + 1;
                    temp[i] = j;
                }
                if (dp[i] > len) {
                    len = dp[i];
                    idx = i;
                }
            }
        }

        vector<int> ans(len, 0);
        int index = len - 1;
        while (index >= 0) {
            ans[index] = nums[idx];
            idx = temp[idx];
            index--;
        }
        return ans;
    }
};
```
