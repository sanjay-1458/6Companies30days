# Problem
<a href="https://leetcode.com/problems/find-the-distance-value-between-two-arrays/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given two integer arrays arr1 and arr2, and the integer d, return the distance value between the two arrays.

The distance value is defined as the number of elements arr1[i] such that there is not any element arr2[j] where |arr1[i]-arr2[j]| <= d.

### Sample Input
```
arr1 = [4,5,8], arr2 = [10,9,1,8], d = 2
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) {
        int n = arr2.size();
        sort(arr2.begin(), arr2.end());
        int res = 0;

        for (int &num:arr1) {
            int low=0,high=n-1;
            while (low<=high) {
                int mid=(low+high)/2;
                if(abs(num-arr2[mid])<=d) {
                    break;
                }
                else if(num<arr2[mid]) {
                    high=mid-1;
                }
                else{
                    low=mid+1;
                }
            }
            if(low>high) {
                res++;
            }
        }

        return res;
    }
};
```
