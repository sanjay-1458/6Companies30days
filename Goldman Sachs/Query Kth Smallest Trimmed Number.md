# Problem
<a href="https://leetcode.com/problems/query-kth-smallest-trimmed-number/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a 0-indexed array of strings nums, where each string is of equal length and consists of only digits.

You are also given a 0-indexed 2D integer array queries where queries[i] = [ki, trimi]. For each queries[i], you need to:

Trim each number in nums to its rightmost trimi digits.
Determine the index of the kith smallest trimmed number in nums. If two trimmed numbers are equal, the number with the lower index is considered to be smaller.
Reset each number in nums to its original length.
Return an array answer of the same length as queries, where answer[i] is the answer to the ith query.

Note:

To trim to the rightmost x digits means to keep removing the leftmost digit, until only x digits remain.
Strings in nums may contain leading zeros.


### Sample Input
```
nums = ["102","473","251","814"], queries = [[1,1],[2,3],[4,2],[1,2]]
```
### Sample Output
```
[2,2,1,0]
```

### Solution
```cpp
class Solution {
public:
    vector<int> smallestTrimmedNumbers(vector<string>& nums, vector<vector<int>>& queries) {
        int maxi = nums[0].size(), n = nums.size();
        
        
        if (all_of(nums.begin(), nums.end(), [&nums](const string& s){ return s == nums[0]; })) {
            vector<int> result(queries.size());
            for (int i = 0; i < queries.size(); ++i) {
                result[i] = queries[i][0] - 1;  
            }
            return result;
        }

        for (int i = 0; i < queries.size(); ++i) {
            queries[i].push_back(i);
        }
        sort(queries.begin(), queries.end(), [](vector<int>&a, vector<int>&b){
            return a[1] < b[1];
        });

        vector<int> ans(queries.size(), 0);
        int j = 0;
        map<string, int> mp;
        for (int i = 0; i < n; ++i) {
            mp[nums[i]] = i;
        }

        for (int l = maxi - 1; l >= 0; --l) {
            vector<int> count(10, 0);
            for (int i = 0; i < n; ++i) {
                count[nums[i][l] - '0']++;
            }
            for (int i = 1; i < 10; ++i) {
                count[i] += count[i - 1];
            }
            vector<string> output(n, "");
            for (int i = n - 1; i >= 0; --i) {
                output[count[nums[i][l] - '0'] - 1] = nums[i];
                count[nums[i][l] - '0']--;
            }
            nums = output;

            while (j < queries.size()) {
                if (maxi - queries[j][1] == l) {
                    ans[queries[j][2]] = mp[nums[queries[j][0] - 1]];
                    j++;
                }
                else {
                    break;
                }
            }
        }
        return ans;
    }
};

```
