# Problem
<a href="https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer array nums and an integer k. Find the maximum subarray sum of all the subarrays of nums that meet the following conditions:

The length of the subarray is k, and
All the elements of the subarray are distinct.
Return the maximum subarray sum of all the subarrays that meet the conditions. If no subarray meets the conditions, return 0.

A subarray is a contiguous non-empty sequence of elements within an array.

### Sample Input
```
nums = [1,5,4,2,9,9,9], k = 3
```
### Sample Output
```
15
```

### Solution
```cpp
class Solution {
public:
    long long maximumSubarraySum(vector<int>& nums, int k) {
        long long ans=0,sum=0;
        unordered_map<int,int> mp;
        int i=0,j=0,n=nums.size();
        while(j<n){
            sum+=nums[j];
            mp[nums[j]]++;
            if(j-i+1<k){
                j++;
            }
            else{
                if(j-i+1==k && mp.size()==k){
                    ans=max(ans,sum);
                    sum-=nums[i];
                    if(--mp[nums[i]]==0){
                        mp.erase(nums[i]);
                    }
                    i++;
                    j++;
                }
                else{
                    while(mp.size()<j-i+1){
                        if(--mp[nums[i]]==0){
                            mp.erase(nums[i]);
                        }
                        sum-=nums[i];
                        i++;
                    }
                    j++;
                }
            }
        }
        return ans;
    }
};
```
