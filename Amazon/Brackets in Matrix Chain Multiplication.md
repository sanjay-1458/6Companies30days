# Problem
<a href="https://www.geeksforgeeks.org/problems/brackets-in-matrix-chain-multiplication1024/1">
  <img src="../lib/gfg-logo.png" width="50"/>
</a>

Given an array arr[] of length n used to denote the dimensions of a series of matrices such that the dimension of i'th matrix is arr[i] * arr[i+1]. There are a total of n-1 matrices. Find the most efficient way to multiply these matrices together. 
As in MCM, you were returning the most effective count but this time return the string which is formed of A - Z (only Uppercase) denoting matrices & Brackets( "(" ")" ) denoting multiplication symbols. For example, if n =11, the matrixes can be denoted as A - K as n<=26 & brackets as multiplication symbols.

NOTE:

Each multiplication is denoted by putting open & closed brackets to the matrices multiplied & also, please note that the order of matrix multiplication matters, as matrix multiplication is non-commutative A*B != B*A
As there can be multiple possible answers, the console would print "true" for the correct string and "false" for the incorrect string. You need to only return a string that performs a minimum number of multiplications.

### Sample Input
```
arr[] = [40, 20, 30, 10, 30]
```
### Sample Output
```
true
```

### Solution
```cpp
//{ Driver Code Starts
// Initial Template for C++
#include <bits/stdc++.h>
using namespace std;


// } Driver Code Ends
// User function Template for C++
class Solution {
    void make(int i,int j,vector<vector<int>>& points,string&res){
        if(i==j){
            res+='A'+i-1;
            return;
        }
        res+='(';
        make(i,points[i][j],points,res);
        make(points[i][j]+1,j,points,res);
        res+=')';
    }
    
  public:
    string matrixChainOrder(vector<int> &arr) {
        // code here
        int n=arr.size();
        vector<vector<int>> dp(n,vector<int>(n,1e9));
        vector<vector<int>> points(n,vector<int>(n,0));
        for(int i=0;i<n;++i){
            dp[i][i]=0;
        }
        for(int i=n-1;i>=1;--i){
            for(int j=i+1;j<n;++j){
                int mini=1e9;
                int breakPoint=i;
                for(int k=i;k<=j-1;++k){
                    int steps=arr[i-1]*arr[k]*arr[j]+dp[i][k]+dp[k+1][j];
                    if(steps<mini){
                        mini=steps;
                        breakPoint=k;
                    }
                }
                points[i][j]=breakPoint;
                dp[i][j]=mini;
            }
        }
        string res="";
        make(1,n-1,points,res);
        // cout<<res;
        return res;
    }
};

//{ Driver Code Starts.

int get(vector<int> &p, int n) {
    int m[n][n], ans = 1e9;
    for (int i = 1; i < n; i++)
        m[i][i] = 0;
    for (int L = 2; L < n; L++) {
        for (int i = 1; i < n - L + 1; i++) {
            m[i][i + L - 1] = INT_MAX;
            for (int k = i; k <= i + L - 2; k++) {
                int q = m[i][k] + m[k + 1][i + L - 1] + p[i - 1] * p[k] * p[i + L - 1];
                if (q < m[i][i + L - 1]) {
                    m[i][i + L - 1] = q;
                }
            }
        }
    }
    return m[1][n - 1];
}

int find(string s, vector<int> &p) {
    vector<pair<int, int>> arr;
    int ans = 0;
    for (auto t : s) {
        if (t == '(') {
            arr.push_back({-1, -1});
        } else if (t == ')') {
            pair<int, int> b = arr.back();
            arr.pop_back();
            pair<int, int> a = arr.back();
            arr.pop_back();
            arr.pop_back();
            arr.push_back({a.first, b.second});
            ans += a.first * a.second * b.second;
        } else {
            arr.push_back({p[int(t - 'A')], p[int(t - 'A') + 1]});
        }
    }
    return ans;
}

int main() {
    int t;
    cin >> t;
    cin.ignore();
    while (t--) {
        string s;
        getline(cin, s);
        stringstream ss(s);
        vector<int> p;
        int x;
        while (ss >> x) {
            p.push_back(x);
        }
        Solution ob;
        string result = ob.matrixChainOrder(p);
        if (find(result, p) == get(p, p.size())) {
            cout << "true" << endl;
        } else {
            cout << "false" << endl;
        }
    }

    return 0;
}
// } Driver Code Ends
```
