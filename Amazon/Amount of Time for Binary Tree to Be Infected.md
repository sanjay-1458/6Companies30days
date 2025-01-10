# Problem
<a href="https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given the root of a binary tree with unique values, and an integer start. At minute 0, an infection starts from the node with value start.

Each minute, a node becomes infected if:

The node is currently uninfected.
The node is adjacent to an infected node.
Return the number of minutes needed for the entire tree to be infected.

...

### Sample Input
```
root = [1,5,3,null,4,10,6,9,2], start = 3

```
### Sample Output
```
4
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
    int amountOfTime(TreeNode* root, int start) {
        // child parent
        map<TreeNode*,TreeNode*> mp;
        queue<TreeNode*> q;
        q.push(root);
        mp[root]=root;
        TreeNode* st=root;
        while(!q.empty()){
            TreeNode* p=q.front();
            q.pop();
            if(p->left!=nullptr){
                q.push(p->left);
                mp[p->left]=p;
            }
            if(p->right!=nullptr){
                q.push(p->right);
                mp[p->right]=p;
            }
            if(p->val==start){
                st=p;
            }
        }
        int cnt=0;
        q.push(st);
        vector<int> vis(100001,0);
        vis[start]=1;
        while(!q.empty()){
            int n=q.size();
            while(n--){
                TreeNode* node=q.front();
                q.pop();
                if(node->left!=nullptr && vis[node->left->val]==0){
                    q.push(node->left);
                    vis[node->left->val]=1;
                }
                if(node->right!=nullptr && vis[node->right->val]==0){
                    q.push(node->right);
                    vis[node->right->val]=1;
                }
                if(mp[node]!=node && vis[mp[node]->val]==0){
                    q.push(mp[node]);
                    vis[mp[node]->val]=1;
                }
            }
            cnt++;
        }
        return cnt-1;
    }
};

```
