# Problem
<a href="https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

There are n cities numbered from 0 to n-1. Given the array edges where edges[i] = [fromi, toi, weighti] represents a bidirectional and weighted edge between cities fromi and toi, and given the integer distanceThreshold.

Return the city with the smallest number of cities that are reachable through some path and whose distance is at most distanceThreshold, If there are multiple such cities, return the city with the greatest number.

Notice that the distance of a path connecting cities i and j is equal to the sum of the edges' weights along that path.

### Sample Input
```
 n = 4, edges = [[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold = 4
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
public:
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        vector<vector<int>> dp(n,vector<int>(n,1e9));
        for(int i=0;i<n;++i) dp[i][i]=0;
        for(auto &x:edges){
            int u=x[0],v=x[1],w=x[2];
            dp[u][v]=w;
            dp[v][u]=w;
        }
        for(int k=0;k<n;++k){
            for(int i=0;i<n;++i){
                for(int j=0;j<n;++j){
                    dp[i][j]=min(dp[i][j],dp[i][k]+dp[k][j]);
                }
            }
        }
        vector<int> v(n,1e9);
        for(int i=0;i<n;++i){
            int cnt=0;
            for(int j=0;j<n;++j){
                if(i==j) continue;
                if(dp[i][j]<=distanceThreshold){
                    cnt++;
                }
            }
            v[i]=cnt;
        }
        int mini=*min_element(v.begin(),v.end());
        int ind=-1;
        for(int i=0;i<n;++i){
            if(v[i]==mini){
                ind=i;
            }
        }
        return ind;
    }
};
```
