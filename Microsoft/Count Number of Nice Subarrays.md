# Problem
<a href="https://leetcode.com/problems/count-number-of-nice-subarrays/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an array of integers nums and an integer k. A continuous subarray is called nice if there are k odd numbers on it.

Return the number of nice sub-arrays.

### Sample Input
```
nums = [1,1,2,1,1], k = 3
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int k) {
        int n=nums.size();
        int i=0,j=0,ans=0,cnt=0;
        vector<int> suff(n,0);
        for(int j=n-1;j>=0;--j){
            suff[j]=cnt;
            if(!(nums[j]&1)){
                cnt++;
            }
            else{
                cnt=0;
            }
        }
        cnt=0;
        while(j<n){
            if(nums[j]&1){
                cnt++;
            }
            if(cnt<k){
                j++;
            }
            else{
                while(i<n && cnt==k){
                    ans++;
                    ans+=suff[j];
                    if(nums[i]&1){
                        cnt--;
                    }
                    i++;
                }
                j++;
            }
        }
        return ans;
    }
};
```
