# Longest Uncommon Subsequence I

@(算法)

给定两个字符串，你需要从这两个字符串中找出最长的特殊序列。最长特殊序列定义如下：该序列为某字符串独有的最长子序列（即不能是其他字符串的子序列）。

**子序列**可以通过删去字符串中的某些字符实现，但不能改变剩余字符的相对顺序。空序列为所有字符串的子序列，任何字符串为其自身的子序列。

输入为两个字符串，输出最长特殊序列的长度。如果不存在，则返回 -1。

**示例 :**

```powershell
输入: "aba", "cdc"
输出: 3
解析: 最长特殊序列可为 "aba" (或 "cdc")
```

**说明:**

1. 两个字符串长度均小于100。
2. 字符串中的字符仅含有 'a'~'z'。

## 方法：

+ 判断两个字符串是否长度相等，如果相等，如果两个字符串一模一样，则不存在**最长特殊序列**，否则，最长特殊序列为两者任意一个字符串。
+ 如果不相等，则最长特殊序列为两个字符串里面较长的字符串。

```cpp
class Solution {
public:
    int findLUSlength(string a, string b) {
        if (a.length() != b.length())
        {
            return (a.length() > b.length()) ? a.length() : b.length();
        }
        else if (a.compare(b) == 0)
        {
            return -1;
        }
        else
        {
            return a.length();
        }
    }
};
```
