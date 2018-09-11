# Reverse String II

@(算法)

给定一个字符串和一个整数 k，你需要对从字符串开头算起的每个 2k 个字符的前k个字符进行反转。如果剩余少于 k 个字符，则将剩余的所有全部反转。如果有小于 2k 但大于或等于 k 个字符，则反转前 k 个字符，并将剩余的字符保持原样。

**示例:**
```powershell
输入: s = "abcdefg", k = 2
输出: "bacdfeg"
```

**要求:**
1. 该字符串只包含小写的英文字母。
2. 给定字符串的长度和 k 在[1, 10000]范围内。


## 方法：

```cpp
class Solution {
public:
    string reverseStr(string s, int k) {
        int lenS = s.length();
        int tmpLen = lenS;
        int start = 0;
        while (tmpLen > 0)
        {
            if (tmpLen < k)
            {
                reverseStrInner(s, start, lenS - 1);
                break;
            }
            else if (tmpLen >= k && tmpLen < 2 * k)
            {
                reverseStrInner(s, start, start + k - 1);
                break;
            }
            else
            {
                reverseStrInner(s, start, start + k - 1);
                start += 2 * k;
                tmpLen -= 2 * k;
            }
        }
        
        return s;
    }
    
    void reverseStrInner(std::string & s, int start, int end)
    {
        while (start < end)
        {
            char tmp = s[end];
            s[end] = s[start];
            s[start] = tmp;
            start++;
            end--;
        }
    }
};
```




