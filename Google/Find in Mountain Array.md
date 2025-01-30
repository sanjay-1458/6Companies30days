# Problem
<a href="https://leetcode.com/problems/find-in-mountain-array/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

(This problem is an interactive problem.)

You may recall that an array arr is a mountain array if and only if:

arr.length >= 3
There exists some i with 0 < i < arr.length - 1 such that:
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
Given a mountain array mountainArr, return the minimum index such that mountainArr.get(index) == target. If such an index does not exist, return -1.

You cannot access the mountain array directly. You may only access the array using a MountainArray interface:

MountainArray.get(k) returns the element of the array at index k (0-indexed).
MountainArray.length() returns the length of the array.
Submissions making more than 100 calls to MountainArray.get will be judged Wrong Answer. Also, any solutions that attempt to circumvent the judge will result in disqualification.

### Sample Input
```
mountainArr = [1,2,3,4,5,3,1], target = 3
```
### Sample Output
```
2
```

### Solution
```cpp
/**
 * // This is the MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * class MountainArray {
 *   public:
 *     int get(int index);
 *     int length();
 * };
 */

class Solution {
public:
    int findInMountainArray(int target, MountainArray &arr) {
        int n = arr.length();
        int low = 0, high = n - 1;

        while (low < high) {
            int mid = low + (high - low) / 2;
            if (arr.get(mid) > arr.get(mid + 1)) high = mid;
            else low = mid + 1;
        }
        int peak = low;

        low = 0, high = peak;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            int val = arr.get(mid);
            if (val == target) return mid;
            if (val < target) low = mid + 1;
            else high = mid - 1;
        }

        low = peak + 1, high = n - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            int val = arr.get(mid);
            if (val == target) return mid;
            if (val > target) low = mid + 1;
            else high = mid - 1;
        }

        return -1;
    }
};



```
