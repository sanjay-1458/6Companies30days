# Problem
<a href="https://leetcode.com/problems/stone-game-vi/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Alice and Bob take turns playing a game, with Alice starting first.

There are n stones in a pile. On each player's turn, they can remove a stone from the pile and receive points based on the stone's value. Alice and Bob may value the stones differently.

You are given two integer arrays of length n, aliceValues and bobValues. Each aliceValues[i] and bobValues[i] represents how Alice and Bob, respectively, value the ith stone.

The winner is the person with the most points after all the stones are chosen. If both players have the same amount of points, the game results in a draw. Both players will play optimally. Both players know the other's values.

Determine the result of the game, and:

If Alice wins, return 1.
If Bob wins, return -1.
If the game results in a draw, return 0.

...

### Sample Input
```
aliceValues = [1,3], bobValues = [2,1]
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution {
public:
    int stoneGameVI(vector<int>& aliceValues, vector<int>& bobValues) {
        int n=aliceValues.size();
        vector<int> ind(n,0);
        for(int i=0;i<n;++i){
            ind[i]=i;
        }
        sort(ind.begin(),ind.end(),[&](int i,int j){
            return aliceValues[i]+bobValues[i]>aliceValues[j]+bobValues[j];
        });
        int sum1=0,sum2=0;
        for(int i=0;i<n;++i){
            if(i&1){
                sum2+=bobValues[ind[i]];
            }
            else{
                sum1+=aliceValues[ind[i]];
            }
        }
        if(sum1==sum2){
            return 0;
        }
        if(sum1>sum2){
            return 1;
        }
        return -1;
    }
};
```
