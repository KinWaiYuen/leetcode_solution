# Number of Segments in a String

@(算法)

统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

**示例:**
```powershell
输入: "Hello, my name is John"
输出: 5
```

## 方法：

没啥好说。

```python
class Solution(object):
    def countSegments(self, s):
        """
        :type s: str
        :rtype: int
        """
        num = 0
        for word in s.strip().split(" "):
            if word.strip() != "":
                num = num + 1
        return num
```
