# Problem
<a href="https://leetcode.com/problems/minimum-number-of-days-to-disconnect-island/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an m x n binary grid grid where 1 represents land and 0 represents water. An island is a maximal 4-directionally (horizontal or vertical) connected group of 1's.

The grid is said to be connected if we have exactly one island, otherwise is said disconnected.

In one day, we are allowed to change any single land cell (1) into a water cell (0).

Return the minimum number of days to disconnect the grid.


### Sample Input
```
grid = [[0,1,1,0],[0,1,1,0],[0,0,0,0]]
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
    int countCells(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        int cnt = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                cnt += grid[i][j];
            }
        }
        return cnt;
    }

    int bfs(vector<vector<int>> grid) {
        int n = grid.size(), m = grid[0].size();
        vector<vector<int>> directions = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
        queue<pair<int, int>> q;
        
        
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == 1) {
                    q.push({i, j});
                    grid[i][j] = 0; 
                    int cnt = 1;

                    while (!q.empty()) {
                        auto [x, y] = q.front();
                        q.pop();

                        for (const auto& dir : directions) {
                            int nx = x + dir[0], ny = y + dir[1];
                            if (nx >= 0 && nx < n && ny >= 0 && ny < m && grid[nx][ny] == 1) {
                                q.push({nx, ny});
                                grid[nx][ny] = 0; 
                                ++cnt;
                            }
                        }
                    }
                    return cnt;
                }
            }
        }
        return 0; 
    }

public:
    int minDays(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        int totalLand = countCells(grid);
        if(totalLand == 1 || totalLand == 0) return totalLand;
        
        if (bfs(grid) != totalLand) {
            return 0;
        }

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == 1) {
                    grid[i][j] = 0;
                    if (bfs(grid) != totalLand - 1) {
                        return 1; 
                    }
                    grid[i][j] = 1; 
                }
            }
        }

        
        return 2;
    }
};

```
