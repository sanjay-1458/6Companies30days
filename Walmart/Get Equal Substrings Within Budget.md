# Problem
<a href="https://leetcode.com/problems/get-equal-substrings-within-budget/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given two strings s and t of the same length and an integer maxCost.

You want to change s to t. Changing the ith character of s to ith character of t costs |s[i] - t[i]| (i.e., the absolute difference between the ASCII values of the characters).

Return the maximum length of a substring of s that can be changed to be the same as the corresponding substring of t with a cost less than or equal to maxCost. If there is no substring from s that can be changed to its corresponding substring from t, return 0.


### Sample Input
```
s = "abcd", t = "bcdf", maxCost = 3
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
public:
    int equalSubstring(string s, string t, int maxCost) {
        vector<int> cost;
        int n=s.size();
        int ans=0;
        vector<int> pre(n,0);
        for(int i=0;i<n;++i){
            if(s[i]!=t[i]){
                pre[i]=abs(s[i]-t[i]);
            }
        }
        int i=0,j=0;
        int sum=0;
        while(j<n){
            sum+=pre[j];
            if(sum<=maxCost){
                ans=max(ans,j-i+1);
                j++;
            }
            else{
                while(sum>maxCost){
                    sum-=pre[i];
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
