# Problem
<a href="https://leetcode.com/problems/random-flip-matrix/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

There is an m x n binary grid matrix with all the values set 0 initially. Design an algorithm to randomly pick an index (i, j) where matrix[i][j] == 0 and flips it to 1. All the indices (i, j) where matrix[i][j] == 0 should be equally likely to be returned.

Optimize your algorithm to minimize the number of calls made to the built-in random function of your language and optimize the time and space complexity.

Implement the Solution class:

Solution(int m, int n) Initializes the object with the size of the binary matrix m and n.
int[] flip() Returns a random index [i, j] of the matrix where matrix[i][j] == 0 and flips it to 1.
void reset() Resets all the values of the matrix to be 0.

### Sample Input
```
["Solution", "flip", "flip", "flip", "reset", "flip"]
[[3, 1], [], [], [], [], []]
```
### Sample Output
```
[null, [1, 0], [2, 0], [0, 0], null, [2, 0]]
```

### Solution
```cpp
class Solution {
private:
    int m, n, total;
    unordered_map<int, int> map;

public:
    Solution(int m, int n) : m(m), n(n), total(m * n) {}

    vector<int> flip() {
        int rand_index = rand() % total;
        int x = map.count(rand_index) ? map[rand_index] : rand_index;
        map[rand_index] = map.count(total - 1) ? map[total - 1] : total - 1;
        total--;
        return {x / n, x % n};
    }

    void reset() {
        total = m * n;
        map.clear();
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(m, n);
 * vector<int> param_1 = obj->flip();
 * obj->reset();
 */

```
