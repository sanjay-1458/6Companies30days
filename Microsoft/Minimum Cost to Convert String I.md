# Problem
<a href="https://leetcode.com/problems/minimum-cost-to-convert-string-i/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given two 0-indexed strings source and target, both of length n and consisting of lowercase English letters. You are also given two 0-indexed character arrays original and changed, and an integer array cost, where cost[i] represents the cost of changing the character original[i] to the character changed[i].

You start with the string source. In one operation, you can pick a character x from the string and change it to the character y at a cost of z if there exists any index j such that cost[j] == z, original[j] == x, and changed[j] == y.

Return the minimum cost to convert the string source to the string target using any number of operations. If it is impossible to convert source to target, return -1.

Note that there may exist indices i, j such that original[j] == original[i] and changed[j] == changed[i].

### Sample Input
```
source = "abcd", target = "acbe", original = ["a","b","c","c","e","d"], changed = ["b","c","b","e","b","e"], cost = [2,5,5,1,2,20]
```
### Sample Output
```
28
```

### Solution
```cpp
class Solution {
public:
    long long minimumCost(string source, string target, vector<char>& original, vector<char>& changed, vector<int>& cost) {
        int n=source.size(),m=original.size();
        vector<vector<long long>> v(26,vector<long long>(26,1e9));
        for(size_t i=0;i<26;++i) v[i][i]=0;
        long long ans=0;
        for(size_t i=0;i<m;++i){
            int a=original[i]-'a',b=changed[i]-'a';
            v[a][b]=min(v[a][b],cost[i]*1LL);
        }
        for(size_t k=0;k<26;++k){
            for(size_t i=0;i<26;++i){
                for(size_t j=0;j<26;++j){
                    v[i][j]=min(v[i][j],v[i][k]+v[k][j]);
                }
            }
        }
        for(size_t i=0;i<n;++i){
            int a=source[i]-'a',b=target[i]-'a';
            if(v[a][b]==1e9){
                return -1;
            }
            else{
                ans+=v[a][b];
            }
        }
        return ans;

    }
};
```
