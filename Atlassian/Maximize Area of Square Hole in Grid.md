# Problem
<a href="https://leetcode.com/problems/maximize-area-of-square-hole-in-grid/">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

You are given the two integers, n and m and two integer arrays, hBars and vBars. The grid has n + 2 horizontal and m + 2 vertical bars, creating 1 x 1 unit cells. The bars are indexed starting from 1.

You can remove some of the bars in hBars from horizontal bars and some of the bars in vBars from vertical bars. Note that other bars are fixed and cannot be removed.

Return an integer denoting the maximum area of a square-shaped hole in the grid, after removing some bars (possibly none).

### Sample Input
```
n = 2, m = 1, hBars = [2,3], vBars = [2]
```
### Sample Output
```
4
```

### Solution
```cpp
class Solution {
    int fun(vector<int>& bars) {
        int maxi = 1, cnt = 1;
        sort(bars.begin(), bars.end());

        for (size_t i = 1; i < bars.size(); ++i) {
            if (bars[i] == bars[i - 1] + 1) {
                cnt++;
            } else {
                maxi = max(maxi, cnt);
                cnt = 1;
            }
        }

        return max(maxi, cnt);
    }
public:
    int maximizeSquareHoleArea(int n, int m, vector<int>& hBars, vector<int>& vBars) {
        int up = fun(hBars);
        int left = fun(vBars);

        return (min(up, left) + 1) * (min(up, left) + 1);   
    }
};
```
