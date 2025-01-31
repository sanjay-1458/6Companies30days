# Problem
<a href="https://leetcode.com/problems/count-subtrees-with-max-distance-between-cities/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

There are n cities numbered from 1 to n. You are given an array edges of size n-1, where edges[i] = [ui, vi] represents a bidirectional edge between cities ui and vi. There exists a unique path between each pair of cities. In other words, the cities form a tree.

A subtree is a subset of cities where every city is reachable from every other city in the subset, where the path between each pair passes through only the cities from the subset. Two subtrees are different if there is a city in one subtree that is not present in the other.

For each d from 1 to n-1, find the number of subtrees in which the maximum distance between any two cities in the subtree is equal to d.

Return an array of size n-1 where the dth element (1-indexed) is the number of subtrees in which the maximum distance between any two cities is equal to d.

Notice that the distance between the two cities is the number of edges in the path between them.

### Sample Input
```
n = 4, edges = [[1,2],[2,3],[2,4]]
```
### Sample Output
```
[3,4,0]
```

### Solution
```cpp
struct BFS {
    int last;
    int distance;
    bool isValid;
};

int countSetBits(int mask) {
    int count = 0;
    while (mask) {
        count += (mask & 1);
        mask >>= 1;
    }
    return count;
}

BFS bfs(int startNode, unordered_map<int, bool>& inSubset, const vector<vector<int>>& adj) {
    unordered_map<int, bool> visited;
    queue<int> q;
    q.push(startNode);
    visited[startNode] = true;
    int last = -1, farthestDist = 0;

    while (!q.empty()) {
        int size = q.size();
        for (int i = 0; i < size; ++i) {
            int u = q.front();
            q.pop();
            last = u;

            for (int v : adj[u]) {
                if (inSubset[v] && !visited[v]) {
                    visited[v] = true;
                    q.push(v);
                }
            }
        }
        farthestDist++;
    }

    bool isValid = (visited.size() == inSubset.size());

    BFS result;
    result.last = last;
    result.distance = farthestDist - 1;
    result.isValid = isValid;

    return result;
}

int getMaxDistance(int mask, int n, const vector<vector<int>>& adj) {
    int start = -1;
    unordered_map<int, bool> inSubset;

    for (int src = 0; src < n; ++src) {
        if (mask & (1 << src)) {
            start = src;
            inSubset[src] = true;
        }
    }

    if (start == -1) return -1;

    BFS firstBFS = bfs(start, inSubset, adj);
    if (!firstBFS.isValid) return -1;

    BFS secondBFS = bfs(firstBFS.last, inSubset, adj);
    return secondBFS.distance;
}

class Solution {
public:
    vector<int> countSubgraphsForEachDiameter(int n, vector<vector<int>>& edges) {
        vector<vector<int>> adj(n);
        for (const auto& edge : edges) {
            int u = edge[0] - 1;
            int v = edge[1] - 1;
            adj[u].push_back(v);
            adj[v].push_back(u);
        }

        vector<int> res(n - 1, 0);

        auto maxDistance = [&](int mask) -> int {
            int start = -1;
            unordered_map<int, bool> citiesInSubset;

            for (int src = 0; src < n; ++src) {
                if (mask & (1 << src)) {
                    start = src;
                    citiesInSubset[src] = true;
                }
            }

            if (start == -1) return -1;

            auto bfs = [&](int start) -> BFS {
                unordered_map<int, bool> visited;
                queue<int> q;
                q.push(start);
                visited[start] = true;
                int last = -1, farthestDist = 0;

                while (!q.empty()) {
                    int size = q.size();
                    for (int i = 0; i < size; ++i) {
                        int u = q.front();
                        q.pop();
                        last = u;

                        for (int v : adj[u]) {
                            if (citiesInSubset.find(v) == citiesInSubset.end()) continue;
                            if (visited.find(v) != visited.end()) continue;
                            visited[v] = true;
                            q.push(v);
                        }
                    }
                    farthestDist++;
                }

                bool isValid = (visited.size() == citiesInSubset.size());
                return {last, farthestDist - 1, isValid};
            };

            BFS firstBFS = bfs(start);
            if (!firstBFS.isValid) return -1;

            BFS secondBFS = bfs(firstBFS.last);
            return secondBFS.distance;
        };

        for (int mask = 1; mask < (1 << n); ++mask) {
            int d = maxDistance(mask);
            if (d > 0) res[d - 1]++;
        }

        return res;
    }
};

```
