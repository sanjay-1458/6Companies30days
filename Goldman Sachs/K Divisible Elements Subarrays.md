# Problem
<a href="https://leetcode.com/problems/k-divisible-elements-subarrays/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an integer array nums and two integers k and p, return the number of distinct subarrays, which have at most k elements that are divisible by p.

Two arrays nums1 and nums2 are said to be distinct if:

They are of different lengths, or
There exists at least one index i where nums1[i] != nums2[i].
A subarray is defined as a non-empty contiguous sequence of elements in an array.

### Sample Input
```
nums = [2,3,3,2,2], k = 2, p = 2
```
### Sample Output
```
11
```

### Solution
```cpp
class Solution {
public:
    int countDistinct(vector<int>& nums, int k, int p) {
        unordered_set<string> st;

        for (int i = 0; i < nums.size(); ++i) {
            int cnt = 0;
            string w = "";
            for (int j = i; j < nums.size(); ++j) {
                if (nums[j] % p == 0) cnt++;
                if (cnt <= k) {
                    w += to_string(nums[j]) + ",";
                    st.insert(w);
                } else {
                    break;
                }
            }
        }

        return st.size();
    }
};


```
