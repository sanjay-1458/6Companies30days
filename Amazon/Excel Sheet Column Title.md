# Problem
<a href="https://leetcode.com/problems/excel-sheet-column-title/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

For example:

A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...

### Sample Input
```
columnNumber = 1

```
### Sample Output
```
"A"
```

### Solution
```cpp
class Solution {
    string reverse(string num){
        int low=0,high=num.size()-1;
        while(low<=high){
            swap(num[low],num[high]);
            low++;
            high--;
        }
        return num;
    }
public:
    string convertToTitle(int num) {
        string ans="";
        while(num>0){
            int rem=num%26;
            if(num%26==0){
                ans+='A'+25;
                num--;
            }
            else{
                ans+='A'+rem-1;
            }
            num=num/26;
        }
        ans=reverse(ans);
        return ans;
    }
};

```
