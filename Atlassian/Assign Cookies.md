# Problem
<a href="https://leetcode.com/problems/assign-cookies/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

### Sample Input
```
g = [1,2,3], s = [1,1]
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int i = 0;
        for(int j=0; i<g.size() && j<s.size(); j++)
	        if(g[i]<=s[j]) i++;
        return i;
    }
};
```
