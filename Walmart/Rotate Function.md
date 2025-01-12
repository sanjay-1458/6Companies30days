# Problem
<a href="https://leetcode.com/problems/rotate-function/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer array nums of length n.

Assume arrk to be an array obtained by rotating nums by k positions clock-wise. We define the rotation function F on nums as follow:

F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1].
Return the maximum value of F(0), F(1), ..., F(n-1).

The test cases are generated so that the answer fits in a 32-bit integer.

### Sample Input
```
nums = [4,3,2,6]
```
### Sample Output
```
26
```

### Solution
```cpp
class Solution {
public:
    int maxRotateFunction(vector<int>& nums) {
        int n=nums.size();
        vector<int> dp(n,0);
        int sum=accumulate(nums.begin(),nums.end(),0);
        for(int i=0;i<n;++i){
            dp[0]+=nums[i]*i;
        }
        int ans=dp[0];
        for(int i=1;i<n;++i){
            dp[i]=dp[i-1]+sum-nums[n-i]*(n);

            ans=max(ans,dp[i]);
        }
        return ans;
    }
};
```
