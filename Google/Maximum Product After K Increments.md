# Problem
<a href="https://leetcode.com/problems/maximum-product-after-k-increments/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an array of non-negative integers nums and an integer k. In one operation, you may choose any element from nums and increment it by 1.

Return the maximum product of nums after at most k operations. Since the answer may be very large, return it modulo 109 + 7. Note that you should maximize the product before taking the modulo. 

...

### Sample Input
```
nums = [0,4], k = 5
```
### Sample Output
```
20
```

### Solution
```cpp
class Solution {
public:
    int maximumProduct(vector<int>& nums, int k) {
        priority_queue<int,vector<int>,greater<int>> pq(nums.begin(),nums.end());
        while(k--){
            int x=pq.top();
            pq.pop();
            x++;
            pq.push(x);
        }
        long long prod=1;
        while(!pq.empty()){
            prod=(prod*pq.top()*1LL)%((long long)1e9+7);
            pq.pop();
        }
        return prod%((long long)1e9+7);
    }
};
```
