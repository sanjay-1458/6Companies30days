# Problem
<a href="https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Given a binary tree root, return the maximum sum of all keys of any sub-tree which is also a Binary Search Tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

### Sample Input
```
root = [1,4,3,2,4,2,5,null,null,null,null,null,null,4,6]
```
### Sample Output
```
20
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
public:
    struct Node {
        int sum, mini, maxi;
        bool bst;
    };
    
    Node fun(TreeNode* root, int& ans) {
        if (!root) return {0, INT_MAX, INT_MIN, true};

        auto left = fun(root->left, ans);
        auto right = fun(root->right, ans);

        if (left.bst && right.bst && (root->val > left.maxi) && (root->val < right.mini)) {
            int currSum = left.sum + right.sum + root->val;
            ans = max(ans, currSum);
            return {currSum, min(root->val, left.mini), max(root->val, right.maxi), true};
        }

        return {0, 0, 0, false};
    }

    int maxSumBST(TreeNode* root) {
        int ans = 0;
        fun(root, ans);
        return ans;
    }
};


```
