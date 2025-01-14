# Problem
<a href="https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

One way to serialize a binary tree is to use preorder traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as '#'.


For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where '#' represents a null node.

Given a string of comma-separated values preorder, return true if it is a correct preorder traversal serialization of a binary tree.

It is guaranteed that each comma-separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid.

For example, it could never contain two consecutive commas, such as "1,,3".
Note: You are not allowed to reconstruct the tree.

### Sample Input
```
preorder = "9,3,4,#,#,1,#,#,2,#,6,#,#"
```
### Sample Output
```
true
```

### Solution
```cpp
class Solution {
public:
    bool isValidSerialization(string preorder) {
        vector<string> nodes;
        int pos = 0;
        while ((pos = preorder.find(",")) != string::npos) {
            nodes.push_back(preorder.substr(0, pos));
            preorder.erase(0, pos + 1);
        }
        nodes.push_back(preorder);

        int idx = 0;
        return preorderTraversal(nodes, idx) == nodes.size();
    }

private:
    int preorderTraversal(vector<string>& nodes, int idx) {
        if (idx >= nodes.size() || nodes[idx] == "#") {
            return idx + 1; 
        }
        
        idx = preorderTraversal(nodes, idx + 1);
        
        return preorderTraversal(nodes, idx);
    }
};

```
