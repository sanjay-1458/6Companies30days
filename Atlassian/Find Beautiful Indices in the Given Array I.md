# Problem
<a href="https://leetcode.com/problems/find-beautiful-indices-in-the-given-array-i/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a 0-indexed string s, a string a, a string b, and an integer k.

An index i is beautiful if:

0 <= i <= s.length - a.length
s[i..(i + a.length - 1)] == a
There exists an index j such that:
0 <= j <= s.length - b.length
s[j..(j + b.length - 1)] == b
|j - i| <= k
Return the array that contains beautiful indices in sorted order from smallest to largest.

### Sample Input
```
s = "isawsquirrelnearmysquirrelhouseohmy", a = "my", b = "squirrel", k = 15
```
### Sample Output
```
[16,33]
```

### Solution
```cpp
class Solution {
    vector<int> findOccurrences(string &s, string &p) {
        vector<int> ind;
        int n = s.size(), m = p.size();

        for (int i = 0; i <= n - m; i++) {
            bool match = true;
            for (int j = 0; j < m; j++) {
                if (s[i + j] != p[j]) {
                    match = false;
                    break;
                }
            }
            if (match) ind.push_back(i);
        }
        return ind;
    }

    int lower(vector<int> &arr, int target) {
        int left = 0, right = arr.size(), result = arr.size();
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] >= target) {
                result = mid;
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return result;
    }
public:
    vector<int> beautifulIndices(string s, string a, string b, int k) {
        vector<int> va = findOccurrences(s, a);
        vector<int> vb = findOccurrences(s, b);
        vector<int> ans;
        
        if (vb.empty()) return ans;

        for (int i : va) {
            int idx = lower(vb, i - k);
            if (idx < vb.size() && vb[idx] <= i + k) {
                ans.push_back(i);
            }
        }
        
        return ans;
    }
};
```
