# Problem
<a href="https://leetcode.com/problems/kth-largest-element-in-a-stream/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are part of a university admissions office and need to keep track of the kth highest test score from applicants in real-time. This helps to determine cut-off marks for interviews and admissions dynamically as new applicants submit their scores.

You are tasked to implement a class which, for a given integer k, maintains a stream of test scores and continuously returns the kth highest test score after a new score has been submitted. More specifically, we are looking for the kth highest score in the sorted list of all scores.

Implement the KthLargest class:

KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of test scores nums.
int add(int val) Adds a new test score val to the stream and returns the element representing the kth largest element in the pool of test scores so far.

...

### Sample Input
```
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
```
### Sample Output
```
[null, 4, 5, 5, 8, 8]
```

### Solution
```cpp
class KthLargest {
public:
    priority_queue<int,vector<int>,greater<int>> pq;
    int size=0;
    KthLargest(int k, vector<int>& nums) {
        for(int i=0;i<nums.size();++i){
            pq.push(nums[i]);
            if(pq.size()>k){
                pq.pop();
            }
        }
        size=k;
    }
    
    int add(int val) {
        pq.push(val);
        if(pq.size()>size)
            pq.pop();
        return pq.top();
    }
};

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest* obj = new KthLargest(k, nums);
 * int param_1 = obj->add(val);
 */
```
