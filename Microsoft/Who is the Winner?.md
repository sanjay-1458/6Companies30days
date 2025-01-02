# Who is the Winner? 
<a href="https://leetcode.com/problems/find-the-winner-of-the-circular-game/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

There are n friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to n in clockwise order. More formally, moving clockwise from the ith friend brings you to the (i+1)th friend for 1 <= i < n, and moving clockwise from the nth friend brings you to the 1st friend.

The rules of the game are as follows:

Start at the 1st friend.
1. Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.
2. The last friend you counted leaves the circle and loses the game.
3. If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
4. Else, the last friend in the circle wins the game.
   
Given the number of friends, n, and an integer k, return the winner of the game.

### Sample Input
```
n = 5, k = 2
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
public:
    int findTheWinner(int n, int k) {
        vector<int> v;
        for(int i=1;i<=n;++i){
            v.push_back(i);
        }
        int prev=0;
        while(true){
            if(v.size()==1){
                break;
            }
            int ind=(prev+k-1)%(v.size());
            prev=ind;
            v.erase(v.begin()+ind);
        }
        return v[0];
    }
};
```
