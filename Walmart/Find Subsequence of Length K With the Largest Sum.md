# Envelopes and Dolls
<a href="https://leetcode.com/problems/image-smoother/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer array nums and an integer k. You want to find a subsequence of nums of length k that has the largest sum.

Return any such subsequence as an integer array of length k.

A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

### Sample Input
```
nums = [2,1,3,3], k = 2
```
### Sample Output
```
[3,3]
```

### Solution
```cpp
class Solution {
public:
    vector<int> maxSubsequence(vector<int>& nums, int k) {
        vector<vector<int>> v;
        vector<int> ans;
        int n=nums.size();
        for(int i=0;i<n;++i){
            v.push_back({nums[i],i});
        }
        sort(v.begin(),v.end());
        v.erase(v.begin(),v.begin()+n-k);
        sort(v.begin(),v.end(),[](vector<int>&a,vector<int>&b){
            return a[1]<b[1];
        });
        for(auto x:v){
            ans.push_back(x[0]);
        }
        return ans;
    }
};
```
