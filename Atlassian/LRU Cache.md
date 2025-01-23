# Problem
<a href="https://leetcode.com/problems/lru-cache/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:

LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
int get(int key) Return the value of the key if the key exists, otherwise return -1.
void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
The functions get and put must each run in O(1) average time complexity.

### Sample Input
```
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
```
### Sample Output
```
[null, null, null, 1, null, -1, null, -1, 3, 4]
```

### Solution
```cpp
class Node {
public:
    int key;
    int val;
    Node* next;
    Node* prev;

    Node(int key, int val) {
        this->key = key;
        this->val = val;
        this->next = NULL;
        this->prev = NULL;
    }
};

class LRUCache {
public:

    int left_capacity;
    unordered_map<int, Node*> cache;
    Node *head, *tail;

    LRUCache(int capacity) {
        left_capacity = capacity;
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head->next = tail;
        tail->prev = head;
    }

    void add_node(Node* new_node) {
        
        Node* tail_prev = tail->prev;

        tail_prev->next = new_node;
        new_node->prev = tail_prev;
        new_node->next = tail;
        tail->prev = new_node;
    }

    void delete_node(Node* del_node) {
        Node* prev = del_node->prev;
        Node* next = del_node->next;

        prev->next = next;
        next->prev = prev;
    }
    
    int get(int key) {
        if(cache.find(key) != cache.end()) {
            Node* node = cache[key];
            delete_node(node);
            add_node(node);

            return node->val;
        }

        return -1;
    }
    
    void put(int key, int value) {
        if(cache.find(key) != cache.end()) {
            Node* node = cache[key];
            node->val = value;

            delete_node(node);
            add_node(node);
        } else {
            if(left_capacity == 0) {
                Node* least_recent_node = head->next;
                cache.erase(least_recent_node->key);
                delete_node(least_recent_node); 
            }

            Node* new_node = new Node(key, value);
            add_node(new_node);
            cache[key] = new_node;

            left_capacity -= left_capacity == 0 ? 0 : 1;
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
