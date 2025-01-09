# Problem
<a href="https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

### Sample Input
```
root = [1,2,3,null,null,4,5]
```
### Sample Output
```
[1,2,3,null,null,4,5]
```

### Solution
```cpp
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(!root) return "#,";
        return to_string(root->val) + "," + serialize(root->left) + serialize(root->right);
    }
    
    int num(string &data, int &idx){
        string s = "";
        while(data[idx] != ','){
            s += data[idx];
            idx++;
        }
        idx++;
        if(s == "#") return INT_MIN;
        return stoi(s);
    }

    TreeNode* solve(string &data, int &idx){
        int val = num(data,idx);
        TreeNode* ans =( val == INT_MIN) ? NULL : new TreeNode(val);
        if(ans){
            ans->left = solve(data,idx);
            ans->right = solve(data,idx);
        } 
        return ans;
    }
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        int idx = 0;
        return solve(data,idx);
    }
};
```
