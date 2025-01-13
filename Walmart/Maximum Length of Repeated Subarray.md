# Problem
<a href="https://leetcode.com/problems/maximum-length-of-repeated-subarray/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given two integer arrays nums1 and nums2, return the maximum length of a subarray that appears in both arrays.

### Sample Input
```
nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
    bool check(int k,vector<int>& nums1, vector<int>& nums2){
        set<string> st;
        int n=nums1.size();
        string s="";
        int i=0,j=0;
        while(j<n){
            s+=nums1[j]+'0';
            if(j-i+1<k){
                j++;
            }
            else{
                st.insert(s.substr(i,j-i+1));
                i++;
                j++;
            }
        }
        int m=nums2.size();
        i=0,j=0;
        s="";
        while(j<m){
            s+=nums2[j]+'0';
            if(j-i+1<k){
                j++;
            }
            else{
                if(st.find(s.substr(i,j-i+1))!=st.end()){
                    return true;
                }
                i++;
                j++;
            }
        }
        return false;
    }
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n=nums1.size();
        int l=1,h=n;
        while(l<=h){
            int m=(l+h)/2;
            if(check(m,nums1,nums2)){
                l=m+1;
            }
            else{
                h=m-1;
            }
        }
        return h;
    }
};
```
