# Problem
<a href="https://leetcode.com/problems/top-k-frequent-words/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given an array of strings words and an integer k, return the k most frequent strings.

Return the answer sorted by the frequency from highest to lowest. Sort the words with the same frequency by their lexicographical order.

### Sample Input
```
words = ["i","love","leetcode","i","love","coding"], k = 2
```
### Sample Output
```
["i","love"]
```

### Solution
```cpp
class Comp{
    public:
    bool operator()(pair<int,string>&a,pair<int,string>&b){
        if(a.first>b.first){
            return true;
        }
        else if(a.first==b.first && a.second<b.second){
            return true;
        }
        else{
            return false;
        }
    }
};
class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {
        map<string,int> mp;
        for(auto&x:words){
            mp[x]++;
        }
        priority_queue<pair<int,string>,vector<pair<int,string>>,Comp> pq;
        for(auto &x:mp){
            pq.push({x.second,x.first});
            if(pq.size()>k){
                pq.pop();
            }
        }
        vector<string> ans;
        while(!pq.empty()){
            ans.push_back(pq.top().second);
            pq.pop();
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```
