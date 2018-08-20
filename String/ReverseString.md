# Reverse String

@(算法)

编写一个函数，其作用是将输入的字符串反转过来。

**示例 1:**
```powshell
输入: "hello"
输出: "olleh"
```

**示例 2:**
```powershell
输入: "A man, a plan, a canal: Panama"
输出: "amanaP :lanac a ,nalp a ,nam A"
```

## 方法

```cpp
class Solution {
public:
    string reverseString(string s) {
        int length = s.length();
        int halfLength = (length + 1) / 2;
        for (int i = 0; i < halfLength; i++)
        {
            auto temp = s[i];
            s[i] = s[length - 1 - i];
            s[length - 1 - i] = temp;
        }
        return s;
    }
};
```
