# Envelopes and Dolls
<a href="https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an integer array nums of size n, return the minimum number of moves required to make all array elements equal.

In one move, you can increment or decrement an element of the array by 1.

Test cases are designed so that the answer will fit in a 32-bit integer.

Note: You cannot rotate an envelope.

### Sample Input
```
nums = [1,2,3]
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        int n=nums.size(),ans=0;
        sort(nums.begin(),nums.end());
        int median=0;
        if(n%2==0){
            median=(nums[n/2-1]+nums[n/2])/2;
        }
        else{
            median=nums[n/2];
        }
        for(int i:nums){
            ans+=abs(i-median);
        }
        return ans;
    }
};
```
