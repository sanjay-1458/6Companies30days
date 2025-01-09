# Problem
<a href="https://www.geeksforgeeks.org/problems/nuts-and-bolts-problem0431/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given a set of n nuts & bolts. There is a one-on-one mapping between nuts and bolts. You have to Match nuts and bolts efficiently. Comparison of a nut to another nut or a bolt to another bolt is not allowed. It means the nut can only be compared with the bolt and the bolt can only be compared with the nut to see which one is bigger/smaller.
The elements should follow the following order: { !,#,$,%,&,*,?,@,^ }

Note: Make all the required changes directly in the given arrays, output will be handled by the driver code.

### Sample Input
```
n = 5, nuts[] = {@, %, $, #, ^}, bolts[] = {%, @, #, $ ^}
```
### Sample Output
```
# $ % @ ^
# $ % @ ^
```

### Solution
```cpp
//{ Driver Code Starts
#include <bits/stdc++.h>

using namespace std;


// } Driver Code Ends
// User function template for C++
class Solution {
  public:

    void matchPairs(int n, char nuts[], char bolts[]) {
        // code here
        map<char,char> mp;
        mp['!']='0';
        mp['#']='1';
        mp['$']='2';
        mp['%']='3';
        mp['&']='4';
        mp['*']='5';
        mp['?']='6';
        mp['@']='7';
        mp['^']='8';
        sort(nuts,nuts+n,[&mp](char a,char b){
            return mp[a]<mp[b];
        });
        sort(bolts,bolts+n,[&mp](char a,char b){
            return mp[a]<mp[b];
        });
    }
};

//{ Driver Code Starts.

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        char nuts[n], bolts[n];
        for (int i = 0; i < n; i++) {
            cin >> nuts[i];
        }
        for (int i = 0; i < n; i++) {
            cin >> bolts[i];
        }
        Solution ob;
        ob.matchPairs(n, nuts, bolts);
        for (int i = 0; i < n; i++) {
            cout << nuts[i] << " ";
        }
        cout << "\n";
        for (int i = 0; i < n; i++) {
            cout << bolts[i] << " ";
        }
        cout << "\n";
    
cout << "~" << "\n";
}
    return 0;
}

// } Driver Code Ends
```
