# Problem
<a href="https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given an array arr[] of integers and an integer k, your task is to find the maximum value for each contiguous subarray of size k. The output should be an array of maximum values corresponding to each contiguous subarray.

### Sample Input
```
arr[] = [1, 2, 3, 1, 4, 5, 2, 3, 6], k = 3
```
### Sample Output
```
[3, 3, 4, 5, 5, 5, 6] 
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
    // Function to find maximum of each subarray of size k.
    vector<int> maxOfSubarrays(vector<int>& arr, int k) {
        // code here
        deque<int> dq;
        vector<int> ans;
        int n=arr.size();
        int i=0,j=0;
        while(j<n){
            while(!dq.empty() && arr[j]>dq.back()){
                dq.pop_back();
            }
            dq.push_back(arr[j]);
            if(j-i+1<k){
                j++;
            }
            else{
                ans.push_back(dq.front());
                if(dq.front()==arr[i]){
                    dq.pop_front();
                }
                i++;
                j++;
            }
        }
        return ans;
    }
};

//{ Driver Code Starts.

int main() {
    int t;
    cin >> t;
    cin.ignore(); // Ignore newline character after t

    while (t--) {
        vector<int> arr;
        int k;
        string inputLine;

        getline(cin, inputLine); // Read the array input as a line
        stringstream ss(inputLine);
        int value;
        while (ss >> value) {
            arr.push_back(value);
        }

        cin >> k;
        cin.ignore(); // Ignore newline character after k input

        Solution obj;
        vector<int> res = obj.maxOfSubarrays(arr, k);
        for (int i = 0; i < res.size(); i++)
            cout << res[i] << " ";
        cout << endl;
        cout << "~"
             << "\n";
    }

    return 0;
}

// } Driver Code Ends
```
