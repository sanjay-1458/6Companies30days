# Problem
<a href="https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer array nums and an integer k.

The frequency of an element x is the number of times it occurs in an array.

An array is called good if the frequency of each element in this array is less than or equal to k.

Return the length of the longest good subarray of nums.

A subarray is a contiguous non-empty sequence of elements within an array.

 

### Sample Input
```
nums = [1,2,3,1,2,3,1,2], k = 2
```
### Sample Output
```
6
```

### Solution
```cpp
class Solution {
public:
    int maxSubarrayLength(vector<int>& nums, int k) {
        int n=nums.size();
        int i=0,j=0;
        int ans=0;
        unordered_map<int,int> mp;
        while(j<n){
            bool flag=false;
            int el=nums[j];
            mp[el]++;
            if(mp[el]>k){
                flag=true;
            }
            if(flag==false){
                ans=max(ans,j-i+1);
                j++;
            }
            else{
                while(mp[el]>k){
                    mp[nums[i]]--;
                    i++;
                }
                ans=max(ans,j-i+1);
                j++;
            }
        }
        return ans;
    }
};
```
