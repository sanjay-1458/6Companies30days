# Problem
<a href="https://leetcode.com/problems/map-of-highest-peak/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer matrix isWater of size m x n that represents a map of land and water cells.

If isWater[i][j] == 0, cell (i, j) is a land cell.
If isWater[i][j] == 1, cell (i, j) is a water cell.
You must assign each cell a height in a way that follows these rules:

The height of each cell must be non-negative.
If the cell is a water cell, its height must be 0.
Any two adjacent cells must have an absolute height difference of at most 1. A cell is adjacent to another cell if the former is directly north, east, south, or west of the latter (i.e., their sides are touching).
Find an assignment of heights such that the maximum height in the matrix is maximized.

Return an integer matrix height of size m x n where height[i][j] is cell (i, j)'s height. If there are multiple solutions, return any of them.

### Sample Input
```
isWater = [[0,1],[0,0]]
```
### Sample Output
```
[[1,0],[2,1]]
```

### Solution
```cpp
class Solution {
public:
    vector<vector<int>> highestPeak(vector<vector<int>>& isWater) {
        int m = isWater.size();
        int n = isWater[0].size();
        queue<pair<int, pair<int, int>>> pq;

        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (isWater[i][j] == 1) {
                    isWater[i][j] = 0;
                    pq.push({1, {i, j}});
                } else {
                    isWater[i][j] = -1;
                }
            }
        }

        vector<pair<int, int>> directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        
        while (!pq.empty()) {
            auto [p, cell] = pq.front();
            pq.pop();
            int r = cell.first;
            int c = cell.second;

            for (int i = 0; i < 4; ++i) {
                int nr = r + directions[i].first;
                int nc = c + directions[i].second;
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && isWater[nr][nc] == -1) {
                    pq.push({p + 1, {nr, nc}});
                    isWater[nr][nc] = p;
                }
            }
        }

        return isWater;
    }
};



```
