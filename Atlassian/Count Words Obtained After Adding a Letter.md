# Problem
<a href="https://leetcode.com/problems/count-words-obtained-after-adding-a-letter/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

ou are given two 0-indexed arrays of strings startWords and targetWords. Each string consists of lowercase English letters only.

For each string in targetWords, check if it is possible to choose a string from startWords and perform a conversion operation on it to be equal to that from targetWords.

The conversion operation is described in the following two steps:

Append any lowercase letter that is not present in the string to its end.
For example, if the string is "abc", the letters 'd', 'e', or 'y' can be added to it, but not 'a'. If 'd' is added, the resulting string will be "abcd".
Rearrange the letters of the new string in any arbitrary order.
For example, "abcd" can be rearranged to "acbd", "bacd", "cbda", and so on. Note that it can also be rearranged to "abcd" itself.
Return the number of strings in targetWords that can be obtained by performing the operations on any string of startWords.

Note that you will only be verifying if the string in targetWords can be obtained from a string in startWords by performing the operations. The strings in startWords do not actually change during this process.

...

### Sample Input
```
startWords = ["ant","act","tack"], targetWords = ["tack","act","acti"]
```
### Sample Output
```
2
```

### Solution
```cpp
class Solution {
public:
    string sortString(const string& str) {
        string sortedStr = str;
        sort(sortedStr.begin(), sortedStr.end());
        return sortedStr;
    }

    unordered_map<string, int> createTargetMap(const vector<string>& target) {
        unordered_map<string, int> mp;
        for (const string& t : target) {
            mp[sortString(t)]++;
        }
        return mp;
    }

    int countValidTransformations(const string& startStr, unordered_map<string, int>& mp) {
        int arr[26] = {0};
        for (char c : startStr) {
            arr[c - 'a']++;
        }

        int ans = 0;
        for (int j = 0; j < 26; j++) {
            string dum = startStr;
            if (arr[j] == 0) {
                dum += 'a' + j;
                string sortedDum = sortString(dum);
                if (mp.find(sortedDum) != mp.end()) {
                    ans += mp[sortedDum];
                    mp.erase(sortedDum);
                }
            }
        }
        return ans;
    }

    int wordCount(vector<string>& startWords, vector<string>& targetWords) {
        unordered_map<string, int> targetMap = createTargetMap(targetWords);
        int ans = 0;

        for (const string& startStr : startWords) {
            ans += countValidTransformations(startStr, targetMap);
        }

        return ans;
    }
};

```
