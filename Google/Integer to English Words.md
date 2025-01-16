# Problem
<a href="https://leetcode.com/problems/integer-to-english-words/description/">
  <img src="../lib/leetcode-3628885-3030025.webp" width="50"/>
</a>

Convert a non-negative integer num to its English words representation.

...

### Sample Input
```
num = 123
```
### Sample Output
```
"One Hundred Twenty Three"
```

### Solution
```cpp
class Solution {
public:
string convertUnderThousand(int num, vector<string>& belowTwenty, vector<string>& tens) {
        string result = "";
        
        if (num >= 100) {
            result += belowTwenty[num / 100] + " Hundred ";
            num %= 100;
        }
        
        if (num >= 20) {
            result += tens[num / 10] + " ";
            num %= 10;
        }
        
        if (num > 0) {
            result += belowTwenty[num] + " ";
        }
        
        return result;
    }
    string numberToWords(int num) {
        if (num == 0) return "Zero";
        
        vector<string> belowTwenty = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
        vector<string> tens = {"", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
        vector<string> scale = {"", "Thousand", "Million", "Billion"};
        
        string result = "";
        int scaleIndex = 0;
        
        while (num > 0) {
            if (num % 1000 != 0) {
                result = convertUnderThousand(num % 1000, belowTwenty, tens) + scale[scaleIndex] + " " + result;
            }
            num /= 1000;
            scaleIndex++;
        }
        
        result.erase(result.find_last_not_of(" ") + 1); 
        return result;
    }
};
```
