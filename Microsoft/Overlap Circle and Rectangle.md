# Overlap Circle and Rectangle.md
<a href="https://leetcode.com/problems/circle-and-rectangle-overlapping/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a number and its reverse. Find that number raised to the power of its own reverse.You are given a circle represented as (radius, xCenter, yCenter) and an axis-aligned rectangle represented as (x1, y1, x2, y2), where (x1, y1) are the coordinates of the bottom-left corner, and (x2, y2) are the coordinates of the top-right corner of the rectangle.

Return true if the circle and rectangle are overlapped otherwise return false. In other words, check if there is any point (xi, yi) that belongs to the circle and the rectangle at the same time.


### Sample Input
```
radius = 1, xCenter = 0, yCenter = 0, x1 = 1, y1 = -1, x2 = 3, y2 = 1
```
### Sample Output
```
true
```

### Solution
```cpp
class Solution {
public:
    bool checkOverlap(int radius, int xCenter, int yCenter, int x1, int y1, int x2, int y2) {
        x1-=xCenter,x2-=xCenter,y1-=yCenter,y2-=yCenter;
        xCenter=0,yCenter=0;
        int nx=0,ny=0;
        if(xCenter<=x1){
            nx=x1;
        }
        else if(xCenter>=x2){
            nx=x2;
        }
        else{
            nx=xCenter;
        }
        if(yCenter<=y1){
            ny=y1;
        }
        else if(yCenter>=y2){
            ny=y2;
        }
        else{
            ny=yCenter;
        }
        return nx*nx+ny*ny<=radius*radius;
    }
};
```

