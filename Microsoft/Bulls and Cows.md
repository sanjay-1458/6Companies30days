# Problem
<a href="https://leetcode.com/problems/bulls-and-cows/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

1. The number of "bulls", which are digits in the guess that are in the correct position.
2. The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

### Sample Input
```
secret = "1807", guess = "7810"
```
### Sample Output
```
"1A3B"
```

### Solution
```cpp
class Solution {
public:
    string getHint(string secret, string guess) {
        int cows=0,n=secret.size();
        for(int i=0;i<n;++i){
            if(secret[i]==guess[i]){
                cows++;
                secret[i]='$';
                guess[i]='$';
            }
        }
        string s="";
        s+=to_string(cows);
        s+='A';
        vector<int> curr(10,0),next(10,0);
        for(char c:secret){
            if(c!='$'){
                curr[c-'0']++;
            }
        }
        for(char c:guess){
            if(c!='$'){
                next[c-'0']++;
            }
        }
        int bulls=0;
        for(int i=0;i<=9;++i){
            bulls+=min(curr[i],next[i]);
        }
        s+=to_string(bulls);
        s+='B';
        return s;
    }
};
```
