# Problem
<a href="https://leetcode.com/problems/destroying-asteroids/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an integer mass, which represents the original mass of a planet. You are further given an integer array asteroids, where asteroids[i] is the mass of the ith asteroid.

You can arrange for the planet to collide with the asteroids in any arbitrary order. If the mass of the planet is greater than or equal to the mass of the asteroid, the asteroid is destroyed and the planet gains the mass of the asteroid. Otherwise, the planet is destroyed.

Return true if all asteroids can be destroyed. Otherwise, return false.

...

### Sample Input
```
mass = 10, asteroids = [3,9,19,5,21]
```
### Sample Output
```
true
```

### Solution
```cpp
class Solution {
public:
    bool asteroidsDestroyed(long long int mass, vector<int>& asteroids) {
        sort(asteroids.begin(),asteroids.end());
        int n=asteroids.size();
        for(int i=0;i<n;++i){
            if(mass>=asteroids[i]){
                mass+=asteroids[i];
            }
            else{
                return false;
            }
        }
        return true;
    }
};
```
