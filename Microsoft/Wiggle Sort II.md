# Problem
<a href="https://leetcode.com/problems/wiggle-sort-ii/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an integer array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

You may assume the input array always has a valid answer.

### Sample Input
```
nums = [1,5,1,1,6,4]
```
### Sample Output
```
[1,6,1,5,1,4]
```

### Solution
```cpp
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        int n=nums.size();
        vector<int> temp(nums.begin(),nums.end());
        sort(temp.begin(),temp.end());
        int j=n-1,i=1;
        while(i<n){
            nums[i]=temp[j];
            j--;
            i+=2;
        }
        i=0;
        while(i<n){
            nums[i]=temp[j];
            j--;
            i+=2;
        }
    }
};
```
