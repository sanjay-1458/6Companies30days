# Problem
<a href="https://leetcode.com/problems/merge-k-sorted-lists/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

...

### Sample Input
```
lists = [[1,4,5],[1,3,4],[2,6]]
```
### Sample Output
```
[1,1,2,3,4,4,5,6]
```

### Solution
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Comp{
    public:
    bool operator()(ListNode*below,ListNode*above){
        return below->val>above->val;
    }
};
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.empty()){
            return nullptr;
        }
        priority_queue<ListNode*,vector<ListNode*>,Comp> pq;
        for(const auto&x:lists){
            if(x!=nullptr)
            pq.push(x);
        }
        ListNode *curr=nullptr,*ptr=nullptr;
        while(!pq.empty()){
            ListNode*temp=pq.top();
            if(temp==nullptr){
                break;
            }
            pq.pop();
            if(ptr==nullptr){
                curr=new ListNode(temp->val);
                temp=temp->next;
                ptr=curr;
            }
            else{
                ptr->next=new ListNode(temp->val);
                temp=temp->next;
                ptr=ptr->next;
            }
            if(temp!=nullptr){
                pq.push(temp);
            }
        }
        return curr;
    }
};
```
