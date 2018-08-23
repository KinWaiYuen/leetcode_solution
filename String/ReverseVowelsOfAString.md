# Reverse Vowels of a String

@(算法)

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

**示例 1:**
```powershell
输入: "hello"
输出: "holle"
```

**示例 2:**
```powershell
输入: "leetcode"
输出: "leotcede"
```

**说明:**
元音字母不包含字母"y"。

## 方法：

没啥好说的。

```cpp
class Solution {
public:
    string reverseVowels(string s) {
        std::deque<int> dequeIndex;
        
        for (int i = 0; i < s.length(); i++)
        {
            if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i' || s[i] == 'o' || s[i] == 'u'
              || s[i] == 'A' || s[i] == 'E' || s[i] == 'I' || s[i] == 'O' || s[i] == 'U')
            {
                dequeIndex.push_back(i);
            }
        }
        
        while (!dequeIndex.empty())
        {
            int frontIndex = dequeIndex.front();
            int backIndex = dequeIndex.back();
            
            char cValue = s[frontIndex];
            s[frontIndex] = s[backIndex];
            s[backIndex] = cValue;
            
            dequeIndex.pop_front();
            if (!dequeIndex.empty())
            {
                dequeIndex.pop_back();
            }
        }
        
        return s;
    }
};
```
