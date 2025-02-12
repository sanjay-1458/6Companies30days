# Problem
<a href="https://leetcode.com/problems/minimum-non-zero-product-of-the-array-elements/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given a positive integer p. Consider an array nums (1-indexed) that consists of the integers in the inclusive range [1, 2p - 1] in their binary representations. You are allowed to do the following operation any number of times:

Choose two elements x and y from nums.
Choose a bit in x and swap it with its corresponding bit in y. Corresponding bit refers to the bit that is in the same position in the other integer.
For example, if x = 1101 and y = 0011, after swapping the 2nd bit from the right, we have x = 1111 and y = 0001.

Find the minimum non-zero product of nums after performing the above operation any number of times. Return this product modulo 109 + 7.

Note: The answer should be the minimum product before the modulo operation is done.

### Sample Input
```
p = 1
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution {
public:
    long long fun(long long base, long long exp, int MOD) {
        long long result = 1;
        while (exp > 0) {
            if (exp % 2 == 1) {
                result = (result * base) % MOD;
            }
            base = (base * base) % MOD;
            exp /= 2;
        }
        return result;
    }

    int minNonZeroProduct(int p) {
        int MOD = 1e9 + 7;
        long long num = (1LL << p) - 1;
        long long cnt = num / 2;
        long long pow = fun(num - 1, cnt, MOD);
        
        return (pow * (num % MOD)) % MOD;
    }
};

```
