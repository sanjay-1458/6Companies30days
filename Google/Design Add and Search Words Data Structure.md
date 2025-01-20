# Problem
<a href="https://leetcode.com/problems/design-add-and-search-words-data-structure/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

WordDictionary() Initializes the object.
void addWord(word) Adds word to the data structure, it can be matched later.
bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.
...

### Sample Input
```
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
```
### Sample Output
```
[null,null,null,null,false,true,true,true]
```

### Solution
```cpp
class TrieNode {
public:
    TrieNode* child[26];
    bool isEnd;
    TrieNode() {
        for (int i = 0; i < 26; ++i) {
            child[i] = nullptr;
        }
        isEnd = false;
    }
    bool containKey(char ch) {
        return (child[ch - 'a'] != nullptr);
    }
    void put(char ch, TrieNode* node) {
        child[ch - 'a'] = node;
    }
    TrieNode* get(char ch) {
        return child[ch - 'a'];
    }
    void setEnd() {
        isEnd = true;
    }
    bool getEnd() {
        return isEnd;
    }
};

class Trie {
    TrieNode* root;
public:
    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* node = root;
        for (int i = 0; i < word.size(); ++i) {
            if (!node->containKey(word[i])) {
                node->put(word[i], new TrieNode());
            }
            node = node->get(word[i]);
        }
        node->setEnd();
    }

    bool search(string word, TrieNode* node, int index) {
        if (index == word.size()) {
            return node->getEnd();
        }
        char ch = word[index];
        if (ch == '.') {
            for (int i = 0; i < 26; ++i) {
                if (node->child[i] != nullptr) {
                    if (search(word, node->child[i], index + 1)) {
                        return true;
                    }
                }
            }
            return false;
        } else {
            if (node->containKey(ch)) {
                return search(word, node->get(ch), index + 1);
            } else {
                return false;
            }
        }
    }

    bool search(string word) {
        return search(word, root, 0);
    }
};

class WordDictionary {
public:
    Trie trie;
    WordDictionary() {
    }

    void addWord(string word) {
        trie.insert(word);
    }

    bool search(string word) {
        return trie.search(word);
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */

```
