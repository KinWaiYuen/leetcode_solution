# Add Binary

@(算法)

给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为非空字符串且只包含数字 `1` 和 `0`。

**示例 1:**
```powershell
输入: a = "11", b = "1"
输出: "100"
```

**示例 2:**
```powershell
输入: a = "1010", b = "1011"
输出: "10101"
```

## 方法

```cpp
class Solution {
public:
    string addBinary(string a, string b) {
        int aIndex = a.length() - 1;
        int bIndex = b.length() - 1;
        std::string sResult;
        int next = 0;
        int result = 0;
        
        while (aIndex >= 0 || bIndex >= 0)
        {
            if (aIndex < 0)
            {
                result = ((b[bIndex] - '0') + next) % 2;
                next = ((b[bIndex] - '0') + next) / 2;
                bIndex--;
            }
            else if (bIndex < 0)
            {
                result = ((a[aIndex] - '0') + next) % 2;
                next = ((a[aIndex] - '0') + next) / 2;
                aIndex--;
            }
            else
            {
                result = ((a[aIndex] - '0') + (b[bIndex] - '0') + next) % 2;
                next = ((a[aIndex] - '0') + (b[bIndex] - '0') + next) / 2;
                bIndex--;
                aIndex--;
            }
            sResult = std::to_string(result) + sResult;
        }
        if (next)
        {
            sResult = std::to_string(next) + sResult;
        }
        return sResult;
    }
};
```
