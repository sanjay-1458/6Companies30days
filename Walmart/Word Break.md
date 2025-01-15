# Problem
<a href="https://leetcode.com/problems/word-break/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

### Sample Input
```
s = "leetcode", wordDict = ["leet","code"]
```
### Sample Output
```
true
```

### Solution
```cpp
class Solution {
    int fun(int i,string&s,set<string>&st,vector<int>&dp){
        int n=s.size();
        if(i==n){
            return 0;
        }
        if(dp[i]!=-1){
            return dp[i];
        }
        int pick=0,notPick=fun(i+1,s,st,dp);
        for(int j=i;j<n;++j){
            string temp=s.substr(i,j-i+1);
            if(st.find(temp)!=st.end()){
                int curr=temp.size()+fun(j+1,s,st,dp);
                pick=max(pick,curr);
            }
        }
        return dp[i]=max(pick,notPick);
    }
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n=s.size();
        set<string> st;
        for(auto& x:wordDict){
            st.insert(x);
        }
        vector<int> dp(n,-1);
        return n==fun(0,s,st,dp);
    }
};
```
