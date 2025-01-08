# Problem
<a href="https://leetcode.com/problems/find-number-of-ways-to-reach-the-k-th-stair/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a non-negative integer k. There exists a staircase with an infinite number of stairs, with the lowest stair numbered 0.

Alice has an integer jump, with an initial value of 0. She starts on stair 1 and wants to reach stair k using any number of operations. If she is on stair i, in one operation she can:

Go down to stair i - 1. This operation cannot be used consecutively or on stair 0.
Go up to stair i + 2jump. And then, jump becomes jump + 1.
Return the total number of ways Alice can reach stair k.

Note that it is possible that Alice reaches the stair k, and performs some operations to reach the stair k again.


### Sample Input
```
k = 0
```
### Sample Output
```
0
```

### Solution
```cpp
class Solution {
    int fun(int k,int i,int jump,bool back,map<string,int> &mp){
        if(i>k+1) return 0;
        string ind=to_string(i)+to_string(jump)+to_string(back);
        if(mp.find(ind)!=mp.end()){
            return mp[ind];
        }
        if(i==k){
            if(back==false){
                int x=0,y=0;
                x=fun(k,i+pow(2,jump),jump+1,back,mp);
                if(i!=0){
                    y=fun(k,i-1,jump,true,mp);
                }
                return mp[ind]=1+x+y;
            }
            else{
                return mp[ind]=1+fun(k,i+pow(2,jump),jump+1,false,mp);
            }
        }
        if(back==false){
            int x=0,y=0;
            x=fun(k,i+pow(2,jump),jump+1,back,mp);
            if(i!=0){
                y=fun(k,i-1,jump,true,mp);
            }
            return mp[ind]=x+y;
        }
        else{
            return mp[ind]=fun(k,i+pow(2,jump),jump+1,false,mp);
        }
    }
public:
    int waysToReachStair(int k) {
        map<string,int> mp;
        mp.clear();
        return fun(k,1,0,false,mp);
    }
};
```
