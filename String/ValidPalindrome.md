# Valid Palindrome

@(算法)

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明:** 本题中，我们将空字符串定义为有效的回文串。

**示例 1:**
```powershell
输入: "A man, a plan, a canal: Panama"
输出: true
```

**示例 2:**
```powershell
输入: "race a car"
输出: false
```

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        std::string result;
        for (int i = 0; i < s.length(); i++)
        {
            char c = s[i];
            if (c >= 'A' && c <= 'Z')
            {
                c = 'a' + (c - 'A');
            }
            
            if ((c >= 'a' && c <= 'z') || (c >= '0' && c <= '9'))
            {
                result += c;
            }
        }
        
        for (int i = 0; i < (result.length() + 1) / 2; i++)
        {
            if (result[i] != result[result.length() - 1 - i])
            {
                return false;
            }
        }
        return true;
    }
};
```
