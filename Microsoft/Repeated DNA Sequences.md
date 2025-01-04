# Problem
<a href="https://leetcode.com/problems/repeated-dna-sequences/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'.

For example, "ACGAATTCCG" is a DNA sequence.
When studying DNA, it is useful to identify repeated sequences within the DNA.

Given a string s that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in any order.

### Sample Input
```
s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
```
### Sample Output
```
["AAAAACCCCC","CCCCCAAAAA"]
```

### Solution
```cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        int i=0,j=0,n=s.size();
        map<string,int> mp;
        vector<string> v;
        string temp="";
        while(j<n){
            temp+=s[j];
            if(j-i+1<10){
                j++;
            }
            else{
                mp[temp]++;
                temp.erase(temp.begin());
                i++;
                j++;
            }
        }
        for(const auto&[a,b]:mp){
            if(b>1) v.push_back(a);
        }
        return v;

    }
};
```
