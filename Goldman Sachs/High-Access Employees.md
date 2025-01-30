# Problem
<a href="https://leetcode.com/problems/high-access-employees/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a 2D 0-indexed array of strings, access_times, with size n. For each i where 0 <= i <= n - 1, access_times[i][0] represents the name of an employee, and access_times[i][1] represents the access time of that employee. All entries in access_times are within the same day.

The access time is represented as four digits using a 24-hour time format, for example, "0800" or "2250".

An employee is said to be high-access if he has accessed the system three or more times within a one-hour period.

Times with exactly one hour of difference are not considered part of the same one-hour period. For example, "0815" and "0915" are not part of the same one-hour period.

Access times at the start and end of the day are not counted within the same one-hour period. For example, "0005" and "2350" are not part of the same one-hour period.

Return a list that contains the names of high-access employees with any order you want.

### Sample Input
```
access_times = [["a","0549"],["b","0457"],["a","0532"],["a","0621"],["b","0540"]]
```
### Sample Output
```
["a"]
```

### Solution
```cpp
class Solution {
public:
    vector<string> findHighAccessEmployees(vector<vector<string>>& access_times) {

        sort(access_times.begin(), access_times.end(), [](vector<string>& a, vector<string>& b) {
            return stoi(a[1]) < stoi(b[1]);
        });

        unordered_map<string, deque<int>> mp;
        set<string> v;

        for (auto& x : access_times) {
            string emp = x[0];
            int time = stoi(x[1]);

            mp[emp].push_back(time);

            while(!mp[emp].empty() && time - mp[emp].front() >= 100) {
                mp[emp].pop_front();
            }
            if (mp[emp].size() >= 3) {
                v.insert(emp);
            }
        }
        vector<string> res(v.begin(), v.end());

        return res;
    }
};


```
