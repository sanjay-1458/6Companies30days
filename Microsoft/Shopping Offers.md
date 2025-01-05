# Problem
<a href="https://leetcode.com/problems/shopping-offers/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

In LeetCode Store, there are n items to sell. Each item has a price. However, there are some special offers, and a special offer consists of one or more different kinds of items with a sale price.

You are given an integer array price where price[i] is the price of the ith item, and an integer array needs where needs[i] is the number of pieces of the ith item you want to buy.

You are also given an array special where special[i] is of size n + 1 where special[i][j] is the number of pieces of the jth item in the ith offer and special[i][n] (i.e., the last integer in the array) is the price of the ith offer.

Return the lowest price you have to pay for exactly certain items as given, where you could make optimal use of the special offers. You are not allowed to buy more items than you want, even if that would lower the overall price. You could use any of the special offers as many times as you want.


### Sample Input
```
price = [2,5], special = [[3,0,5],[1,2,10]], needs = [3,2]
```
### Sample Output
```
14
```

### Solution
```cpp
class Solution {
    map<pair<int,vector<int>>,int> mp; 
    int fun(int ind,vector<int>&price,vector<int>&needs,vector<vector<int>>&special){
        int n=special.size(),k=price.size();
        if(ind==n){
            int sum=0;
            for(int i=0;i<k;++i){
                sum+=price[i]*needs[i];
            }
            return sum;
        }
        if(mp.find({ind,needs})!=mp.end()){
            return mp[{ind,needs}];
        }
        vector<int> temp(needs.begin(),needs.end());
        for(int i=0;i<k;++i){
            temp[i]-=special[ind][i];
            if(temp[i]<0){
                return mp[{ind,needs}]=fun(ind+1,price,needs,special);
            }
        }
        return mp[{ind,needs}]=min(fun(ind+1,price,needs,special),fun(ind,price,temp,special)+special[ind][k]);
    }
public:
    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        return fun(0,price,needs,special);
    }
};
```
