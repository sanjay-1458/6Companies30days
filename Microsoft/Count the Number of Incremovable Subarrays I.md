# Problem
<a href="https://leetcode.com/problems/count-the-number-of-incremovable-subarrays-i/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a 0-indexed array of positive integers nums.

A subarray of nums is called incremovable if nums becomes strictly increasing on removing the subarray. For example, the subarray [3, 4] is an incremovable subarray of [5, 3, 4, 6, 7] because removing this subarray changes the array [5, 3, 4, 6, 7] to [5, 6, 7] which is strictly increasing.

Return the total number of incremovable subarrays of nums.

Note that an empty array is considered strictly increasing.

A subarray is a contiguous non-empty sequence of elements within an array.

### Sample Input
```
nums = [1,2,3,4]
```
### Sample Output
```
10
```

### Solution
```cpp
class Solution {
public:
    int incremovableSubarrayCount(vector<int>& nums) {
        int left=-1,right=-1,n=nums.size();
        for(int i=0;i<n-1;++i){
            if(nums[i]>=nums[i+1]){
                left=i;
                break;
            }
        }
        if(left==-1){
            return (n*(n+1))/2;
        }
        for(int i=n-1;i>=0;--i){
            if(nums[i-1]>=nums[i]){
                right=i;
                break;
            }
        }
        int ans=0;
        ans+=n-right+1;
        cout<<ans<<endl;
        ans+=left+1;
        cout<<ans;
        int i=0;
        while(i<=left && right<n){
            if(nums[i]<nums[right]){
                if(i+1!=right){
                    ans++;
                }
                ans+=n-right-1;
                i++;
            }
            else{
                right++;
            }
        }
        return ans;
    }
};
```
