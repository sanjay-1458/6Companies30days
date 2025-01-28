# Problem
<a href="https://www.geeksforgeeks.org/problems/number-following-a-pattern3126/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given a pattern containing only I's and D's. I for increasing and D for decreasing. Devise an algorithm to print the minimum number following that pattern. Digits from 1-9 and digits can't repeat.


### Sample Input
```
D
```
### Sample Output
```
21
```

### Solution
```cpp
//{ Driver Code Starts
#include<bits/stdc++.h> 
using namespace std; 

// } Driver Code Ends
class Solution{   
public:
    string printMinNumberForPattern(string S){
        // code here 
        stack<int> stk;
        string ans = "";
        int curr = 0;
    
        for (int i = 0; i < S.length(); i++) {
            stk.push(i + 1);
    
            if (S[i] == 'I') {
                while (!stk.empty()) {
                    ans += to_string(stk.top());
                    stk.pop();
                }
            }
            curr = i;
        }
    
        stk.push(curr + 2);
        while (!stk.empty()) {
            ans += to_string(stk.top());
            stk.pop();
        }
    
        return ans;
    }
};


//{ Driver Code Starts.
int main() 
{ 
    int t;
    cin>>t;
    while(t--)
    {
        string S;
        cin >> S;
        Solution ob;
        cout << ob.printMinNumberForPattern(S) << endl;
    
cout << "~" << "\n";
}
    return 0; 
} 

// } Driver Code Ends
```
