# Problem
<a href="https://leetcode.com/problems/number-of-good-leaf-nodes-pairs/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given the root of a binary tree and an integer distance. A pair of two different leaf nodes of a binary tree is said to be good if the length of the shortest path between them is less than or equal to distance.

Return the number of good leaf node pairs in the tree.

...

### Sample Input
```
root = [1,2,3,null,4], distance = 3
```
### Sample Output
```
1
```

### Solution
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    int ans=0;
    vector<int> fun(TreeNode*root,int distance){
        if(root->left==nullptr && root->right==nullptr){
            return {1};
        }
        vector<int> left;
        if(root->left)
            left=fun(root->left,distance);
        vector<int> right;
        if(root->right)
            right=fun(root->right,distance);
        int mini=1e9;
        if(!left.empty() && !right.empty()){
            for(auto x:left){
                for(auto y:right){
                    int prod=x+y;
                    mini=min(mini,prod);
                    if(prod<=distance){
                        ans++;
                    }
                }
            }
        }
        vector<int> temp(left.begin(),left.end());
        temp.insert(temp.end(),right.begin(),right.end());
        if(temp.empty()){
            return {};
        }
        for(auto&x:temp){
            x++;
            mini=min(mini,x);
        }
        if(mini>10){
            return {};
        }
        return temp;
    }
public:
    int countPairs(TreeNode* root, int distance) {
        vector<int> t=fun(root,distance);
        
        return ans;
    }
};
```
