# Envelopes and Dolls
<a href="https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an array of non-overlapping axis-aligned rectangles rects where rects[i] = [ai, bi, xi, yi] indicates that (ai, bi) is the bottom-left corner point of the ith rectangle and (xi, yi) is the top-right corner point of the ith rectangle. Design an algorithm to pick a random integer point inside the space covered by one of the given rectangles. A point on the perimeter of a rectangle is included in the space covered by the rectangle.

Any integer point inside the space covered by one of the given rectangles should be equally likely to be returned.

Note that an integer point is a point that has integer coordinates.

Implement the Solution class:

1. Solution(int[][] rects) Initializes the object with the given rectangles rects.
2. int[] pick() Returns a random integer point [u, v] inside the space covered by one of the given rectangles.

### Sample Input
```
["Solution", "pick", "pick", "pick", "pick", "pick"]
[[[[-2, -2, 1, 1], [2, 2, 4, 6]]], [], [], [], [], []]
```
### Sample Output
```
[null, [1, -2], [1, -1], [-1, -2], [-2, -2], [0, 0]]
```

### Solution
```cpp
class Solution {
    int t1=1e9+1,t2=1e9+1,ind=0;
    vector<vector<int>> rects;
public:
    Solution(vector<vector<int>>& rect) {
        rects=rect;
        if(t1==1e9+1){
            t1=rects[ind][0];
            t2=rects[ind][3];
        }
    }
    
    vector<int> pick() {
        int n=rects.size();
        int ai=rects[ind][0],bi=rects[ind][1],xi=rects[ind][2],yi=rects[ind][3];
        vector<int> t;
        if((t1==xi && t2==bi)){
            t.push_back(t1);
            t.push_back(t2);
            ind++;
            if(ind==n) ind=0;
            t1=rects[ind][0],t2=rects[ind][3];
        }
        else{
            t.push_back(t1);
            t.push_back(t2);
            if(t1==xi){
                t2--;
                t1=ai;
            }
            else{
                t1++;
            }
        }
        return t;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(rects);
 * vector<int> param_1 = obj->pick();
 */
```
