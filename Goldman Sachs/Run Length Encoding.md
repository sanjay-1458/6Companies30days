# Problem
<a href="https://www.geeksforgeeks.org/problems/run-length-encoding/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given a string s, Your task is to complete the function encode that returns the run length encoded string for the given string.
eg if the input string is “wwwwaaadexxxxxx”, then the function should return “w4a3d1e1x6″.
You are required to complete the function encode that takes only one argument the string which is to be encoded and returns the encoded string.

### Sample Input
```
s = aaaabbbccc
```
### Sample Output
```
a4b3c3
```

### Solution
```cpp
//{ Driver Code Starts
#include<bits/stdc++.h>
using namespace std;


// } Driver Code Ends

class Solution {
  public:
    string encode(string s) {
        // code here
        string str = "";
        int n = s.size();
    
        for (int i = 0; i < n; i++) {
            int count = 1;
            while (i + 1 < n && s[i] == s[i + 1]) {
                count++;
                i++;
            }
            str += s[i] + to_string(count);
        }
    
        return str;
    }
};


//{ Driver Code Starts.

int main(){
    int t;
    scanf("%d ",&t);
    while(t--){
        
        string s;
        getline(cin,s);
        
        Solution obj;
        string res = obj.encode(s);
        
        cout<<res<<"\n";
        
    
cout << "~" << "\n";
}
}

// } Driver Code Ends```
