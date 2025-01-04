# Problem
<a href="https://leetcode.com/problems/maximum-product-of-the-length-of-two-palindromic-subsequences/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a string s, find two disjoint palindromic subsequences of s such that the product of their lengths is maximized. The two subsequences are disjoint if they do not both pick a character at the same index.

Return the maximum possible product of the lengths of the two palindromic subsequences.

A subsequence is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters. A string is palindromic if it reads the same forward and backward.

### Sample Input
```
s = "leetcodecom"
```
### Sample Output
```
9
```

### Solution
```cpp
class Solution {
    int pal(string& s){
        int n=s.size();
        int low=0,high=n-1;
        while(low<=high){
            if(s[low]==s[high]){
                low++;
                high--;
            }
            else{
                break;
            }
        }
        if(low<=high){
            return 0;
        }else{
            return n;
        }
    }
    int fun(string &s,int ind,string&a,string&b){
        int n=s.size();
        if(ind==n){
            return pal(a)*pal(b);
        }
        a.push_back(s[ind]);
        int pick_a=fun(s,ind+1,a,b);
        a.pop_back();
        b.push_back(s[ind]);
        int pick_b=fun(s,ind+1,a,b);
        b.pop_back();
        int not_pick=fun(s,ind+1,a,b);
        return max(not_pick,max(pick_a,pick_b));
    }
public:
    int maxProduct(string s) {
        int n=s.size();
        string t1="",t2="";
        return fun(s,0,t1,t2);
    }
};
```
