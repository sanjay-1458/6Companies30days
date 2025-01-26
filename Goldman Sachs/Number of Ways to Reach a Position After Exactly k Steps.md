# Problem
<a href="https://leetcode.com/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given two positive integers startPos and endPos. Initially, you are standing at position startPos on an infinite number line. With one step, you can move either one position to the left, or one position to the right.

Given a positive integer k, return the number of different ways to reach the position endPos starting from startPos, such that you perform exactly k steps. Since the answer may be very large, return it modulo 109 + 7.

Two ways are considered different if the order of the steps made is not exactly the same.

Note that the number line includes negative integers.

### Sample Input
```
startPos = 1, endPos = 2, k = 3
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
public:
    const int MOD = 1e9 + 7;

    int numberOfWays(int startPos, int endPos, int k) {
        if (endPos-startPos>k) 
            return 0;

        int len=2*k+1;
        if(0>k+startPos-endPos || k+startPos-endPos>=len) 
            return 0;

        vector<int> prev(len,0), curr(len,0);
        prev[k]=1;

        for(int step=0;step<k;++step){
            for(int i=0;i<len;++i){
                curr[i] = ((i > 0 ? prev[i - 1] : 0) +(i + 1 < len ? prev[i + 1] : 0)) % MOD;
            }
            swap(prev,curr);
        }

        return prev[k+endPos-startPos];
    }
};


```
