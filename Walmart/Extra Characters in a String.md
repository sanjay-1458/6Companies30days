# Problem
<a href="https://leetcode.com/problems/extra-characters-in-a-string/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a 0-indexed string s and a dictionary of words dictionary. You have to break s into one or more non-overlapping substrings such that each substring is present in dictionary. There may be some extra characters in s which are not present in any of the substrings.

Return the minimum number of extra characters left over if you break up s optimally.

### Sample Input
```
s = "leetscode", dictionary = ["leet","code","leetcode"]
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution {
    int fun(int i,string &s, unordered_set<string>& st,vector<int>& dp){
        int n=s.size();
        if(i==n){
            return 0;
        }
        if(dp[i]!=-1) return dp[i];
        int pick=0,notpick=fun(i+1,s,st,dp);
        for(int j=i;j<n;++j){
            string temp=s.substr(i,j-i+1);
            if(st.find(temp)!=st.end()){
                int curr=temp.size()+fun(j+1,s,st,dp);
                pick=max(pick,curr);
            }
        }
        return dp[i]=max(pick,notpick);
    }
public:
    int minExtraChar(string s, vector<string>& dict) {
        int n=s.size();
        unordered_set<string> st;
        for(auto&x:dict){
            st.insert(x);
        }
        vector<int> dp(n,-1);
        return n-fun(0,s,st,dp);
    }
};
```
