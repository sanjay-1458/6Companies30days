# Problem
<a href="https://leetcode.com/problems/sum-of-scores-of-built-strings/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are building a string s of length n one character at a time, prepending each new character to the front of the string. The strings are labeled from 1 to n, where the string with length i is labeled si.

For example, for s = "abaca", s1 == "a", s2 == "ca", s3 == "aca", etc.
The score of si is the length of the longest common prefix between si and sn (Note that s == sn).

Given the final string s, return the sum of the score of every si.

### Sample Input
```
s = "babab"
```
### Sample Output
```
9
```

### Solution
```cpp
class Solution {
public:
    long long sumScores(string s) {
        int n=s.size();
        int l=0,r=1;
        vector<int> z(n,0);
        long long ans=n;
        for(int i=1;i<n;++i){
            if(i+z[i]<r){
                z[i]=z[i-l];
                if(i+z[i]>r){
                    z[i]=r-i;
                }
            }
            while(i+z[i]<n && s[z[i]]==s[i+z[i]]){
                z[i]++;
            }
            if(i+z[i]>r){
                l=i;
                r=z[i]+i;
            }
            ans+=z[i];
        }
        return ans;

    }
};
```
