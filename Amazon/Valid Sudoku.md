# Problem
<a href="https://leetcode.com/problems/valid-sudoku/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.
Note:

A Sudoku board (partially filled) could be valid but is not necessarily solvable.
Only the filled cells need to be validated according to the mentioned rules.

### Sample Input
```
 board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
```
### Sample Output
```
true
```

### Solution
```cpp
class Solution {
    bool row(int i, vector<vector<char>>& board) {
        set<char> s;
        for (int l = 0; l <= 8; ++l) {
            if (board[i][l] != '.') { 
                if (s.find(board[i][l]) == s.end()) {
                    s.insert(board[i][l]);
                } else {
                    return false; 
                }
            }
        }
        return true;
    }

    bool col(int j, vector<vector<char>>& board) {
        set<char> s;
        for (int l = 0; l <= 8; ++l) {
            if (board[l][j] != '.') { 
                if (s.find(board[l][j]) == s.end()) {
                    s.insert(board[l][j]);
                } else {
                    return false;
                }
            }
        }
        return true;
    }

    bool box(int i, int j, vector<vector<char>>& board) {
        set<char> s;
        for (int k = i; k <= i + 2; ++k) {
            for (int l = j; l <= j + 2; ++l) {
                if (board[k][l] != '.') { 
                    if (s.find(board[k][l]) == s.end()) {
                        s.insert(board[k][l]);
                    } else {
                        return false; 
                    }
                }
            }
        }
        return true;
    }

public:
    bool isValidSudoku(vector<vector<char>>& board) {
        for (int i = 0; i <= 8; ++i) {
            if (!row(i, board) || !col(i, board)) {
                return false; 
            }
        }
        for (int i = 0; i <= 6; i += 3) {
            for (int j = 0; j <= 6; j += 3) {
                if (!box(i, j, board)) {
                    return false; 
                }
            }
        }
        return true;
    }
};

```
