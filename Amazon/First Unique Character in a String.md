# Problem
<a href="https://leetcode.com/problems/first-unique-character-in-a-string/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

### Sample Input
```
s = "leetcode"
```
### Sample Output
```
0
```

### Solution
```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<int,int> mp;
        for(const auto& x:s){
            mp[x]++;
        }
        for(size_t i=0;i<s.size();++i){
            if(!(mp[s[i]]-1)){
                return i;
            }
        }
        return -1;
    }
};
```
