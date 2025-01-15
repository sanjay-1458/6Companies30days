# Problem
<a href="https://leetcode.com/problems/battleships-in-a-board/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an m x n matrix board where each cell is a battleship 'X' or empty '.', return the number of the battleships on board.

Battleships can only be placed horizontally or vertically on board. In other words, they can only be made of the shape 1 x k (1 row, k columns) or k x 1 (k rows, 1 column), where k can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).

### Sample Input
```
board = [["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
public:
    int countBattleships(vector<vector<char>>& board) {
        int n=board.size(),m=board[0].size();
        int ans=0;
        for(int i=0;i<n;++i){
            for(int j=0;j<m;++j){
                if(board[i][j]=='X' && (i==0 || board[i-1][j]=='.') && (j==0 || board[i][j-1]=='.')){
                    ans++;
                }
            }
        }
        return ans;
    }
};
```
