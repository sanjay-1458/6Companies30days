# Problem
<a href="https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

### Sample Input
```
digits = "23"
```
### Sample Output
```
["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

### Solution
```cpp
class Solution {
    void fun(int i,string &str,vector<string>&ans,string&t,map<char,string>&mp){
        int n=str.size();
        if(i>=n){
            ans.push_back(t);
            return;
        }
        for(int j=0;j<mp[str[i]].size();++j){
            char x=mp[str[i]][j];
            t.push_back(x);
            fun(i+1,str,ans,t,mp);
            t.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string str) {
        map<char,string> mp;
        if(str.size()==0) return {};
        mp['2']="abc";
        mp['3']="def";
        mp['4']="ghi";
        mp['5']="jkl";
        mp['6']="mno";
        mp['7']="pqrs";
        mp['8']="tuv";
        mp['9']="wxyz";
        vector<string> ans;
        string t="";
        fun(0,str,ans,t,mp);
        return ans;
    }
};
```
