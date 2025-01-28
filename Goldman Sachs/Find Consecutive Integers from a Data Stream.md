# Problem
<a href="https://leetcode.com/problems/find-consecutive-integers-from-a-data-stream/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

For a stream of integers, implement a data structure that checks if the last k integers parsed in the stream are equal to value.

Implement the DataStream class:

DataStream(int value, int k) Initializes the object with an empty integer stream and the two integers value and k.
boolean consec(int num) Adds num to the stream of integers. Returns true if the last k integers are equal to value, and false otherwise. If there are less than k integers, the condition does not hold true, so returns false.

### Sample Input
```
["DataStream", "consec", "consec", "consec", "consec"]
[[4, 3], [4], [4], [4], [3]]
```
### Sample Output
```
[null, false, false, true, false]
```

### Solution
```cpp
class DataStream {
    int K,Val,cnt;
public:
    DataStream(int value, int k) {
        cnt=0,Val=value,K=k;
    }
    
    bool consec(int num) {
        (num==Val)?cnt++:cnt=0;
        return cnt>=K;
    }
};

/**
 * Your DataStream object will be instantiated and called as such:
 * DataStream* obj = new DataStream(value, k);
 * bool param_1 = obj->consec(num);
 */

```
