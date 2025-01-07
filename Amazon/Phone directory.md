# Problem
<a href="https://www.geeksforgeeks.org/problems/phone-directory4628/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given a list of contacts contact[] of length n where each contact is a string which exist in a phone directory and a query string s. The task is to implement a search query for the phone directory. Run a search query for each prefix p of the query string s (i.e. from  index 1 to |s|) that prints all the distinct contacts which have the same prefix as p in lexicographical increasing order. Please refer the explanation part for better understanding.
Note: If there is no match between query and contacts, print "0".

### Sample Input
```
n = 3
contact[] = {"geeikistest", "geeksforgeeks", "geeksfortest"}
s = "geeips"
```
### Sample Output
```
geeikistest geeksforgeeks geeksfortest
geeikistest geeksforgeeks geeksfortest
geeikistest geeksforgeeks geeksfortest
geeikistest
0
0
```

### Solution
```cpp
//{ Driver Code Starts
// Initial Template for C++

#include <bits/stdc++.h>
using namespace std;

// } Driver Code Ends
// User function Template for C++

class Node{
    Node* links[26];
    bool flag=false;
    vector<int> ind;
    public:
    Node(){
        for(int i=0;i<26;++i){
            links[i]=nullptr;
        }
    }
    bool contain(char ch){
        return links[ch-'a']!=nullptr;
    }
    Node *get(char ch){
        return links[ch-'a'];
    }
    void put(char ch,Node *node){
        links[ch-'a']=node;
    }
    void setEnd(){
        flag=true;
    }
    bool isEnd(){
        return flag;
    }
    void putInd(int x){
        ind.push_back(x);
    }
    vector<int> index(){
        return ind;
    }
};
class Trie {
private:
    Node* root;
public:
    Trie() {
        root=new Node();
    }
    
    void insert(string word,int ind) {
        Node *node=root;
        int n=word.size();
        for(int i=0;i<n;++i){
            if(!node->contain(word[i])){
                node->put(word[i],new Node());
            }
            node=node->get(word[i]);
            node->putInd(ind);
        }
        node->setEnd();
    }
    vector<vector<string>> fun(string s,string contact[]){
        Node *node=root;
        vector<vector<string>> ans;
        int n=s.size();
        int cnt=0;
        for(int i=0;i<n;++i){
            vector<string> temp;
            if(node->contain(s[i])){
                node=node->get(s[i]);
                vector<int> index=node->index();
                for(auto x:index){
                    temp.push_back(contact[x]);
                }
                ans.push_back(temp);
                cnt++;
            }
            else{
                break;
            }
        }
        while(cnt<n){
            ans.push_back({"0"});
            cnt++;
        }
        return ans;
        
    }
    
    
};
class Solution{
public:
    vector<vector<string>> displayContacts(int n, string contact[], string s)
    {
        // code here
        Trie trie;
        sort(contact,contact+n);
        n = unique(contact, contact + n) - contact; 
        for(int i=0;i<n;++i){
            trie.insert(contact[i],i);
        }
        return trie.fun(s,contact);
    }
};

//{ Driver Code Starts.

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        string contact[n], s;
        for(int i = 0;i < n;i++)
            cin>>contact[i];
        cin>>s;
        
        Solution ob;
        vector<vector<string>> ans = ob.displayContacts(n, contact, s);
        for(int i = 0;i < ans.size();i++){
            for(auto u: ans[i])
                cout<<u<<" ";
            cout<<"\n";
        }
    
cout << "~" << "\n";
}
    return 0;
}
// } Driver Code Ends
```
