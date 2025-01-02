# Envelopes and Dolls
<a href="https://leetcode.com/problems/find-the-winner-of-the-circular-game/description/">
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
    int lowerBound(vector<vector<int>>& temp, vector<int>& v) {
        int low = 0, high = temp.size() - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (temp[mid][1] < v[1]) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return low;
    }
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        int n=envelopes.size();
        int ans=0;
        vector<vector<int>> temp;
        sort(envelopes.begin(),envelopes.end(),[](vector<int>&a,vector<int>&b){
            if(a[0]==b[0]){
                return a[1]>b[1];
            }
            else{
                return a[0]<b[0];
            }
        });
        for(int i=0;i<n;++i){
            int ind=lowerBound(temp,envelopes[i]);
            if(ind>=temp.size()){
                temp.push_back(envelopes[i]);
            }
            else{
                temp[ind]=envelopes[i];
            }
        }
        return temp.size();
    }
};
```
