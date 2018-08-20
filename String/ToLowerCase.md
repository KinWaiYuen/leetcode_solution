# To Lower Case

@(算法)

实现函数 ToLowerCase()，该函数接收一个字符串参数 str，并将该字符串中的大写字母转换成小写字母，之后返回新的字符串。

**示例 1：**
```powshell
输入: "Hello"
输出: "hello"
```

**示例 2：**
```powershell
输入: "here"
输出: "here"
```

**示例 3：**
```powershell
输入: "LOVELY"
输出: "lovely"
```

## 方法：

没啥好说的，很简单的题目。

```cpp
class Solution {
public:
    string toLowerCase(string str) {
        for (auto & c: str)
        {
            c = (c >= 'A' && c <= 'Z') ? 'a' + (c - 'A') : c;
        }
        return str;
    }
};
```
