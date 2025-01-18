# Problem
<a href="https://leetcode.com/problems/maximum-product-after-k-increments/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a 2D array of integers envelopes where envelopes[i] = [wi, hi] represents the width and the height of an envelope.

One envelope can fit into another if and only if both the width and height of one envelope are greater than the other envelope's width and height.

Return the maximum number of envelopes you can Russian doll (i.e., put one inside the other).

Note: You cannot rotate an envelope.

### Sample Input
```
envelopes = [[5,4],[6,4],[6,7],[2,3]]
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
    int lower(int k,vector<int>&nums){
        int n=nums.size();
        int low=0,high=n-1;
        while(low<=high){
            int mid=(low+high)/2;
            if(nums[mid]<k){
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }
        return low;
    }
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        sort(envelopes.begin(),envelopes.end(),[](vector<int>a,vector<int>b){
            if(a[0]==b[0]){
                return a[1]>b[1];
            }
            else{
                return a[0]<b[0];
            }
        });
        int n=envelopes.size();
        vector<int> temp;
        for(int i=0;i<n;++i){
            int el=envelopes[i][1];
            int ind=lower(el,temp);
            if(ind>=(int)temp.size()) temp.push_back(el);
            else temp[ind]=el;
        }
        return (int)temp.size();
    }
};
```
