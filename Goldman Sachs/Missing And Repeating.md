# Problem
<a href="https://www.geeksforgeeks.org/problems/find-missing-and-repeating2512/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given an unsorted array arr of positive integers. One number a from the set [1, 2,....,n] is missing and one number b occurs twice in the array. Find numbers a and b.

Note: The test cases are generated such that there always exists one missing and one repeating number within the range [1,n].

### Sample Input
```
arr[] = [2, 2]
```
### Sample Output
```
[2, 1]
```

### Solution
```cpp
//{ Driver Code Starts
#include <bits/stdc++.h>

using namespace std;


// } Driver Code Ends
class Solution {
  public:
    vector<int> findTwoElement(vector<int>& arr) {
        int duplicate = 0, missing = 0, n = arr.size();

        for (int i = 0; i < n; i++) {
            int val = abs(arr[i]);
            if (arr[val - 1] < 0) 
                duplicate = val;
            else 
                arr[val - 1] = -arr[val - 1];
        }
    
        for (int i = 0; i < n; i++) {
            if (arr[i] > 0) {
                missing = i + 1;
                break;
            }
        }
    
        return {duplicate, missing};
    }
};

//{ Driver Code Starts.

int main() {
    int t;
    cin >> t;
    cin.ignore();
    while (t--) {
        string input;
        int num;
        vector<int> arr;
        getline(cin, input);
        stringstream s2(input);
        while (s2 >> num) {
            arr.push_back(num);
        }
        Solution ob;
        auto ans = ob.findTwoElement(arr);
        cout << ans[0] << " " << ans[1] << "\n";

        cout << "~"
             << "\n";
    }
    return 0;
}
// } Driver Code Ends
```
