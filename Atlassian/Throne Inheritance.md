# Problem
<a href="https://leetcode.com/problems/throne-inheritance/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

A kingdom consists of a king, his children, his grandchildren, and so on. Every once in a while, someone in the family dies or a child is born.

The kingdom has a well-defined order of inheritance that consists of the king as the first member. Let's define the recursive function Successor(x, curOrder), which given a person x and the inheritance order so far, returns who should be the next person after x in the order of inheritance.

Successor(x, curOrder):
    if x has no children or all of x's children are in curOrder:
        if x is the king return null
        else return Successor(x's parent, curOrder)
    else return x's oldest child who's not in curOrder
For example, assume we have a kingdom that consists of the king, his children Alice and Bob (Alice is older than Bob), and finally Alice's son Jack.

In the beginning, curOrder will be ["king"].
Calling Successor(king, curOrder) will return Alice, so we append to curOrder to get ["king", "Alice"].
Calling Successor(Alice, curOrder) will return Jack, so we append to curOrder to get ["king", "Alice", "Jack"].
Calling Successor(Jack, curOrder) will return Bob, so we append to curOrder to get ["king", "Alice", "Jack", "Bob"].
Calling Successor(Bob, curOrder) will return null. Thus the order of inheritance will be ["king", "Alice", "Jack", "Bob"].
Using the above function, we can always obtain a unique order of inheritance.

Implement the ThroneInheritance class:

ThroneInheritance(string kingName) Initializes an object of the ThroneInheritance class. The name of the king is given as part of the constructor.
void birth(string parentName, string childName) Indicates that parentName gave birth to childName.
void death(string name) Indicates the death of name. The death of the person doesn't affect the Successor function nor the current inheritance order. You can treat it as just marking the person as dead.
string[] getInheritanceOrder() Returns a list representing the current order of inheritance excluding dead people.

### Sample Input
```
["ThroneInheritance", "birth", "birth", "birth", "birth", "birth", "birth", "getInheritanceOrder", "death", "getInheritanceOrder"]
[["king"], ["king", "andy"], ["king", "bob"], ["king", "catherine"], ["andy", "matthew"], ["bob", "alex"], ["bob", "asha"], [null], ["bob"], [null]]
```
### Sample Output
```
[null, null, null, null, null, null, null, ["king", "andy", "matthew", "bob", "alex", "asha", "catherine"], null, ["king", "andy", "matthew", "alex", "asha", "catherine"]]
```

### Solution
```cpp

class ThroneInheritance {
private:
    unordered_map<string, deque<string>> upper;
    unordered_set<string> lower;
    string curr;

public:
    ThroneInheritance(string kingName) {
        curr = kingName;
        upper[kingName] = deque<string>();
    }
    
    void birth(string parentName, string childName) {
        upper[parentName].push_back(childName);
    }
    
    void death(string name) {
        lower.insert(name);
    }
    
    vector<string> getInheritanceOrder() {
        vector<string> order;
        stack<string> dfsStack;
        dfsStack.push(curr);

        while (!dfsStack.empty()) {
            string current = dfsStack.top();
            dfsStack.pop();

            if (!lower.count(current)) {
                order.push_back(current);
            }

            if (upper.find(current) != upper.end()) {
                auto &child = upper[current];
                for (auto it = child.rbegin(); it != child.rend(); ++it) {
                    dfsStack.push(*it);
                }
            }
        }

        return order;
    }
};

/**
 * Your ThroneInheritance object will be instantiated and called as such:
 * ThroneInheritance* obj = new ThroneInheritance(kingName);
 * obj->birth(parentName,childName);
 * obj->death(name);
 * vector<string> param_3 = obj->getInheritanceOrder();
 */
```
