# Problem
<a href="https://leetcode.com/problems/k-diff-pairs-in-an-array/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an array of integers nums and an integer k, return the number of unique k-diff pairs in the array.

A k-diff pair is an integer pair (nums[i], nums[j]), where the following are true:

0 <= i, j < nums.length
i != j
|nums[i] - nums[j]| == k
Notice that |val| denotes the absolute value of val.


### Sample Input
```
nums = [3,1,4,1,5], k = 2
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
public:
    int findPairs(vector<int>& nums, int k) {
        int n=nums.size(),ans=0;
        map<int,int> mp;
        for(int i=0;i<n;++i){
            mp[nums[i]]++;
        }
        for(auto x:mp){
            int b=x.first;
            int f=x.second;
            if(k==0){
                if(f>=2){
                    ans+=2;
                }
            }
            else{
                if(mp.find(b-k)!=mp.end()){
                    ans++;
                } 
                if(mp.find(b+k)!=mp.end()){
                    ans++;
                }
            }
        }
        return ans/2;
    }
};
```
