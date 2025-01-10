# Problem
<a href="https://www.geeksforgeeks.org/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given a linked list, delete n nodes after skipping m nodes of a linked list until the last of the linked list.

### Sample Input
```
Linked List: 9->1->3->5->9->4->10->1, n = 1, m = 2
```
### Sample Output
```
9->1->5->9->10->1
```

### Solution
```cpp
//{ Driver Code Starts
#include <algorithm>
#include <cmath>
#include <cstdio>
#include <ios>
#include <iostream>
#include <random>
#include <sstream>
#include <string>
#include <vector>

using namespace std;

struct Node {
    int data;
    Node* next;

    Node(int x) {
        data = x;
        next = NULL;
    }
};

// Class definition with updated method

/* Function to print nodes in a given linked list */
void printList(Node* head) {
    Node* temp = head;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}


// } Driver Code Ends
/*
delete n nodes after m nodes
  The input list will have at least one element
  Node is defined as

struct Node {
    int data;
    Node *next;

    Node(int x) {
        data = x;
        next = NULL;
    }
};

*/
class Solution {
  public:
    Node* linkdelete(Node* head, int n, int m) {
        Node *temp,*curr=head;
        int d=n,s=m;
        while(curr!=NULL){
            for(int i=1;i<m && curr!=NULL;++i){
                curr=curr->next;
            }
            if(curr==NULL){
                return head;
            }
            Node *nxt=curr->next;
            for(int i=0;i<n && nxt!=NULL;++i){
                Node *temp=nxt;
                nxt=nxt->next;
                temp->next=NULL;
                delete temp;
            }
            curr->next=nxt;
            curr=nxt;
        }
        return head;
    }
};

//{ Driver Code Starts.
int main() {
    int t;
    cin >> t;
    cin.ignore();
    while (t--) {
        vector<int> arr;
        string input;
        getline(cin, input);
        stringstream ss(input);
        int number;
        while (ss >> number) {
            arr.push_back(number);
        }

        vector<int> arr2;
        string input2;
        getline(cin, input2);
        stringstream ss2(input2);
        int number2;
        while (ss2 >> number2) {
            arr2.push_back(number2);
        }

        int n = arr2[0], m = arr2[1];

        if (arr.empty()) {
            cout << "empty" << endl;
            continue;
        }

        Node* head = new Node(arr[0]);
        Node* tail = head;
        for (int i = 1; i < arr.size(); ++i) {
            tail->next = new Node(arr[i]);
            tail = tail->next;
        }

        Solution ob;
        head = ob.linkdelete(head, n, m);
        printList(head);

        // Clean up the remaining nodes to avoid memory leaks
        while (head != NULL) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }
    return 0;
}

// } Driver Code Ends
```
