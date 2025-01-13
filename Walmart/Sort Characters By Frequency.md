# Problem
<a href="https://leetcode.com/problems/sort-characters-by-frequency/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a string s, sort it in decreasing order based on the frequency of the characters. The frequency of a character is the number of times it appears in the string.

Return the sorted string. If there are multiple answers, return any of them.

### Sample Input
```
s = "tree"
```
### Sample Output
```
"eert"
```

### Solution
```cpp
class Solution {
public:
    string frequencySort(string s) {
        vector<pair<int,char>>v;
        map<char,int>mp;
        for(int i=0;i<s.size();i++){
            mp[s[i]]++;
        }
        for(auto i:mp){
            v.push_back({i.second,i.first});
        }
        sort(v.rbegin(),v.rend());

        string ans;
        
        for(auto i:v){
            for(int j=0;j<i.first;j++){
                ans+= i.second;
            }
        }
        return ans;
    }
};
```
