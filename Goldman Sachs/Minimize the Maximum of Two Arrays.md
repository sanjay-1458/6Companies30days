# Problem
<a href="https://leetcode.com/problems/minimize-the-maximum-of-two-arrays/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

We have two arrays arr1 and arr2 which are initially empty. You need to add positive integers to them such that they satisfy all the following conditions:

arr1 contains uniqueCnt1 distinct positive integers, each of which is not divisible by divisor1.
arr2 contains uniqueCnt2 distinct positive integers, each of which is not divisible by divisor2.
No integer is present in both arr1 and arr2.
Given divisor1, divisor2, uniqueCnt1, and uniqueCnt2, return the minimum possible maximum integer that can be present in either array.

### Sample Input
```
divisor1 = 2, divisor2 = 7, uniqueCnt1 = 1, uniqueCnt2 = 3
```
### Sample Output
```
4
```

### Solution
```cpp
class Solution {
    long long gcd(long long a, long long b) {
        return b == 0 ? a : gcd(b, a % b);
    }

    long long lcm(long long a, long long b) {
        return (a / gcd(a, b)) * b;
    }

public:
    int minimizeSet(int divisor1, int divisor2, int uniqueCnt1, int uniqueCnt2) {
        long long lcm_val = lcm(divisor1, divisor2);
        long long left = 1, right = 1e10, ans = right;

        while (left <= right) {
            long long mid = (left + right) / 2;
            long long valid1 = mid - mid / divisor1;
            long long valid2 = mid - mid / divisor2;
            long long total = mid - mid / lcm_val;

            if (valid1 >= uniqueCnt1 && valid2 >= uniqueCnt2 && total >= uniqueCnt1 + uniqueCnt2) {
                ans = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return (int)ans;
    }
};

```
