# Length of Last Word

@(算法)

给定一个仅包含大小写字母和空格 ' ' 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 0 。

**说明：** 一个单词是指由字母组成，但不包含任何空格的字符串。

**示例:**
```powershell
输入: "Hello World"
输出: 5
```

## 方法：

没啥好讲的，一行代码解决。

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        return len(s.strip().split(" ")[-1])
```

