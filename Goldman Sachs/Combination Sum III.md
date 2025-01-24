# Problem
<a href="https://leetcode.com/problems/combination-sum-iii/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Find all valid combinations of k numbers that sum up to n such that the following conditions are true:

Only numbers 1 through 9 are used.
Each number is used at most once.
Return a list of all possible valid combinations. The list must not contain the same combination twice, and the combinations may be returned in any order.

### Sample Input
```
k = 3, n = 7
```
### Sample Output
```
[[1,2,4]]
```

### Solution
```cpp
class Solution {
    void combination(int num, int target, int k, vector<int>& ds, vector<vector<int>>& ans) {
        if (num == 10) {
            if (target == 0 && ds.size() == k) {
                ans.push_back(ds);
            }
            return;
        }

        if (num <= target) {
            ds.push_back(num);
            combination(num + 1, target - num, k, ds, ans);
            ds.pop_back();
        }

        combination(num + 1, target, k, ds, ans);
    }

public:
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> ans;
        if ((k * (k + 1) / 2) > n) return ans;
        vector<int> ds;
        combination(1, n, k, ds, ans);
        return ans;
    }
};

```
