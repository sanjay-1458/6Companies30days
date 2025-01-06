# Problem
<a href="https://leetcode.com/problems/longest-mountain-in-array/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You may recall that an array arr is a mountain array if and only if:

arr.length >= 3
There exists some index i (0-indexed) with 0 < i < arr.length - 1 such that:
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
Given an integer array arr, return the length of the longest subarray, which is a mountain. Return 0 if there is no mountain subarray.

 

### Sample Input
```
arr = [2,1,4,7,3,2,5]
```
### Sample Output
```
5
```

### Solution
```cpp
class Solution {
public:
    int longestMountain(vector<int>& arr) {
        int cnti = 0, cntd = 0, ans = 0, curr = 0, n = arr.size();
        if (n == 3) {
            if (arr[0] < arr[1] && arr[1] > arr[2]) {
                return 3;
            }
            else {
                return 0;
            }
        }
        for (int i = 0; i < n - 1; ++i) {
            if (curr == 0) {
                if (arr[i] < arr[i + 1]) {
                    curr = 1;
                    cnti = 1;  
                    cntd = 0;
                }
                else {
                    cnti = 0;
                    cntd = 0;
                }
            }
            else if (curr == 1) {
                if (arr[i] < arr[i + 1]) {
                    cnti++;
                }
                else if (arr[i] == arr[i + 1]) {
                    curr = 0;
                    cnti = 0;
                    cntd = 0;
                }
                else {
                    cntd++;  
                    curr = 2;
                }
            }
            else if (curr == 2) {
                
                if (i == n - 2 && arr[i] > arr[i + 1]) {
                    cntd++;
                    ans = max(ans, cnti + cntd + 1);
                    break;
                }
                ans = max(ans, cnti + cntd + 1);
                if (arr[i] > arr[i + 1]) {
                    cntd++;  
                }
                else if (arr[i] < arr[i + 1]) {
                    curr = 1;
                    cnti = 1;
                    cntd = 0;
                }
                else {
                    curr = 0;
                    cnti = 0;
                    cntd = 0;
                }
            }

            if (curr == 2) {
                ans = max(ans, cnti + cntd + 1);
            }
        }
        return ans;
    }
};

```
