# Envelopes and Dolls
<a href="https://leetcode.com/problems/image-smoother/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

An image smoother is a filter of the size 3 x 3 that can be applied to each cell of an image by rounding down the average of the cell and the eight surrounding cells (i.e., the average of the nine cells in the blue smoother). If one or more of the surrounding cells of a cell is not present, we do not consider it in the average (i.e., the average of the four cells in the red smoother).

Given an m x n integer matrix img representing the grayscale of an image, return the image after applying the smoother on each cell of it.

### Sample Input
```
img = [[1,1,1],[1,0,1],[1,1,1]]
```
### Sample Output
```
[[0,0,0],[0,0,0],[0,0,0]]
```

### Solution
```cpp
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& img) {
        int n=img.size(),m=img[0].size();
        for(int i=0;i<n;++i){
            for(int j=0;j<m;++j){
                if(i==0 && j==0){
                    //
                }
                else if(i==0){
                    img[i][j]+=img[i][j-1];
                }
                else if(j==0){
                    img[i][j]+=img[i-1][j];
                }
                else{
                    img[i][j]+=img[i-1][j]+img[i][j-1]-img[i-1][j-1];
                }
            }
        }
        vector<vector<int>> ans(n,vector<int>(m,0));
        for(int i=0;i<n;++i){
            for(int j=0;j<m;++j){
                int diag=-1,down=-1,right=-1;
                if(i+1<n && j+1<m){
                    diag=img[i+1][j+1];
                }
                if(i+1<n){
                    down=img[i+1][j];
                }
                if(j+1<m){
                    right=img[i][j+1];
                }
                int sum=0;
                
                if(diag!=-1){
                    int l=0;
                    sum+=diag;
                    l+=4;
                    if(i-2>=0 && j+1<m){
                        sum-=img[i-2][j+1];
                    }
                    if(i+1<n && j-2>=0){
                        sum-=img[i+1][j-2];
                    }
                    if(i-2>=0 && j-2>=0){
                        sum+=img[i-2][j-2];
                    }
                    if(i-1>=0){
                        l+=2;
                    }
                    if(j-1>=0){
                        l+=2;
                    }
                    if(i-1>=0 && j-1>=0){
                        l++;
                    }
                    ans[i][j]=sum/l;
                }
                else if(down!=-1){
                    int l=0;
                    sum+=down;
                    l+=2;
                    if(i+1<n && j-2>=0){
                        sum-=img[i+1][j-2];
                    }
                    if(i-2>=0){
                        sum-=img[i-2][j];
                    }
                    if(i-2>=0 && j-2>=0){
                        sum+=img[i-2][j-2];
                    }
                    if(j-1>=0){
                        l+=2;
                    }
                    if(i-1>=0){
                        l+=1;
                    }
                    if(i-1>=0 && j-1>=0){
                        l++;
                    }
                    ans[i][j]=sum/l;
                }
                else if(right!=-1){
                    sum+=right;
                    int l=0;
                    l+=2;
                    if(i-2>=0 && j+1<m){
                        sum-=img[i-2][j+1];
                    }
                    if(j-2>=0){
                        sum-=img[i][j-2];
                    }
                    if(i-2>=0 && j-2>=0){
                        sum+=img[i-2][j-2];
                    }
                    if(i-1>=0){
                        l+=2;
                    }
                    if(j-1>=0){
                        l+=1;
                    }
                    if(i-1>=0 && j-1>=0){
                        l++;
                    }
                    ans[i][j]=sum/l;
                }
                else{
                    sum+=img[i][j];
                    int l=0;
                    l+=1;
                    if(i-2>=0){
                        sum-=img[i-2][j];
                    }
                    if(j-2>=0){
                        sum-=img[i][j-2];
                    }
                    if(i-2>=0 && j-2>=0){
                        sum+=img[i-2][j-2];
                    }
                    if(i-1>=0){
                        l+=1;
                    }
                    if(j-1>=0){
                        l+=1;
                    }
                    if(i-1>=0 && j-1>=0){
                        l++;
                    }
                    ans[i][j]=sum/l;
                }
            }
        }
        return ans;
    }
};
```
