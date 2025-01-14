# Problem
<a href="https://leetcode.com/problems/friends-of-appropriate-ages/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

There are n persons on a social media website. You are given an integer array ages where ages[i] is the age of the ith person.

A Person x will not send a friend request to a person y (x != y) if any of the following conditions is true:

age[y] <= 0.5 * age[x] + 7
age[y] > age[x]
age[y] > 100 && age[x] < 100
Otherwise, x will send a friend request to y.

Note that if x sends a request to y, y will not necessarily send a request to x. Also, a person will not send a friend request to themself.

Return the total number of friend requests made.

### Sample Input
```
ages = [16,16]
```
### Sample Output
```
2
```

### Solution
```cpp

class Solution {
public:
    int numFriendRequests(vector<int>& ages) {
        int ans = 0;
        sort(ages.begin(), ages.end());
        int n = ages.size();
        unordered_map<int, int> mp;

        for (int i = 0; i < n; ++i) {
            if (mp.find(ages[i]) != mp.end()) {
                ans += mp[ages[i]];
                continue;
            }

            int low = -1;
            int start = 0, end = n - 1;

            while (start <= end) {
                int mid = start + (end - start) / 2;
                if (ages[mid] > 0.5 * ages[i] + 7) {
                    low = mid;
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            }

            if (low < 0) continue;

            int high = -1;
            start = 0, end = n - 1;

            while (start <= end) {
                int mid = start + (end - start) / 2;
                if (ages[mid] <= ages[i]) {
                    high = mid;
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            }

            int count = high - low;
            ans += (count > 0) ? count : 0;
            mp[ages[i]] = (count > 0) ? count : 0;
        }

        return ans;
    }
};

```
