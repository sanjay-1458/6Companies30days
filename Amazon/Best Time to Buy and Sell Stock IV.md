# Problem
<a href="https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer array prices where prices[i] is the price of a given stock on the ith day, and an integer k.

Find the maximum profit you can achieve. You may complete at most k transactions: i.e. you may buy at most k times and sell at most k times.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

### Sample Input
```
k = 2, prices = [2,4,1]
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
    int dp[1001][101][2];
    int fun(int k,int ind,int x,vector<int>&prices){
        int n=prices.size();
        if(k==0 || ind>=n){
            if(x==0)
                return 0;
            else
                return -1e9;
        }
        if(dp[ind][k][x]!=-1) return dp[ind][k][x];
        if(x==0){
            return dp[ind][k][x]=max(-prices[ind]+fun(k,ind+1,1,prices),fun(k,ind+1,0,prices));
        }
        else{
            return dp[ind][k][x]=max(prices[ind]+fun(k-1,ind+1,0,prices),fun(k,ind+1,1,prices));
        }
    }
public:
    int maxProfit(int k, vector<int>& prices) {
        
        memset(dp,-1,sizeof(dp));
        return fun(k,0,0,prices);
    }
};
```
